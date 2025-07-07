
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")

local LocalPlayer = Players.LocalPlayer
local Camera = Workspace.CurrentCamera

-- ===== GUI Setup =====
local ScreenGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
ScreenGui.Name = "AimbotESP_GUI"

local AimbotButton = Instance.new("TextButton", ScreenGui)
AimbotButton.Size = UDim2.new(0, 120, 0, 40)
AimbotButton.Position = UDim2.new(0, 10, 0, 10)
AimbotButton.Text = "Aimbot: OFF"
AimbotButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
AimbotButton.TextScaled = true

local ESPButton = Instance.new("TextButton", ScreenGui)
ESPButton.Size = UDim2.new(0, 120, 0, 40)
ESPButton.Position = UDim2.new(0, 10, 0, 60)
ESPButton.Text = "ESP: OFF"
ESPButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
ESPButton.TextScaled = true

-- ===== Estado dos sistemas =====
local AimbotEnabled = false
local ESPEnabled = false

AimbotButton.MouseButton1Click:Connect(function()
	AimbotEnabled = not AimbotEnabled
	AimbotButton.Text = AimbotEnabled and "Aimbot: ON" or "Aimbot: OFF"
	AimbotButton.BackgroundColor3 = AimbotEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 0, 0)
end)

ESPButton.MouseButton1Click:Connect(function()
	ESPEnabled = not ESPEnabled
	ESPButton.Text = ESPEnabled and "ESP: ON" or "ESP: OFF"
	ESPButton.BackgroundColor3 = ESPEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 0, 0)

	-- Alternar visibilidade dos ESPs já existentes
	for _, label in pairs(ESPLabels) do
		if label and label:IsA("BillboardGui") then
			label.Enabled = ESPEnabled
		end
	end
end)

-- ===== Raycast Setup =====
local rayParams = RaycastParams.new()
rayParams.FilterType = Enum.RaycastFilterType.Blacklist
rayParams.IgnoreWater = true

local function IsVisible(targetPart)
	if not targetPart then return false end
	local origin = Camera.CFrame.Position
	local direction = (targetPart.Position - origin)
	rayParams.FilterDescendantsInstances = {LocalPlayer.Character}
	local result = Workspace:Raycast(origin, direction, rayParams)
	return not result or result.Instance:IsDescendantOf(targetPart.Parent)
end

-- ===== Aimbot Function =====
local function GetClosestVisiblePlayer()
	local closestPlayer = nil
	local shortestDistance = math.huge
	local mouse = LocalPlayer:GetMouse()

	for _, player in pairs(Players:GetPlayers()) do
		if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Head") then
			local head = player.Character.Head
			local screenPoint, onScreen = Camera:WorldToViewportPoint(head.Position)
			if onScreen and IsVisible(head) then
				local distance = (Vector2.new(screenPoint.X, screenPoint.Y) - Vector2.new(mouse.X, mouse.Y)).Magnitude
				if distance < shortestDistance then
					shortestDistance = distance
					closestPlayer = player
				end
			end
		end
	end

	return closestPlayer
end

-- ===== ESP Functionality =====
local ESPFolder = Instance.new("Folder", game.CoreGui)
ESPFolder.Name = "ESP_Labels"

local ESPLabels = {}

local function CreateESPLabel(player)
	local billboard = Instance.new("BillboardGui")
	billboard.Name = "ESPLabel"
	billboard.AlwaysOnTop = true
	billboard.Size = UDim2.new(0, 100, 0, 30)
	billboard.StudsOffset = Vector3.new(0, 3, 0)
	billboard.Enabled = ESPEnabled

	local text = Instance.new("TextLabel", billboard)
	text.Size = UDim2.new(1, 0, 1, 0)
	text.BackgroundTransparency = 1
	text.TextColor3 = Color3.fromRGB(255, 0, 0)
	text.TextStrokeTransparency = 0.5
	text.TextScaled = true
	text.Font = Enum.Font.SourceSansBold
	text.Text = player.Name

	billboard.Parent = ESPFolder
	return billboard
end

-- ===== Main Update Loop =====
RunService.RenderStepped:Connect(function()
	-- Aimbot
	if AimbotEnabled then
		local target = GetClosestVisiblePlayer()
		if target and target.Character and target.Character:FindFirstChild("Head") then
			local head = target.Character.Head.Position
			local look = (head - Camera.CFrame.Position).Unit
			Camera.CFrame = CFrame.new(Camera.CFrame.Position, Camera.CFrame.Position + look)
		end
	end

	-- ESP
	for _, player in pairs(Players:GetPlayers()) do
		if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Head") then
			local head = player.Character.Head
			local screenPoint, onScreen = Camera:WorldToViewportPoint(head.Position)
			local visible = onScreen and IsVisible(head)

			-- Criar label se não existir
			if not ESPLabels[player] then
				local label = CreateESPLabel(player)
				label.Adornee = head
				ESPLabels[player] = label
			end

			-- Atualizar label
			local label = ESPLabels[player]
			label.Adornee = head
			label.Enabled = ESPEnabled and visible
		end
	end

	-- Limpar labels de jogadores que saíram
	for player, label in pairs(ESPLabels) do
		if not Players:FindFirstChild(player.Name) then
			label:Destroy()
			ESPLabels[player] = nil
		end
	end
end)
