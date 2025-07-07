-- Aimbot GUI
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")

local LocalPlayer = Players.LocalPlayer
local Camera = Workspace.CurrentCamera

-- Criar GUI
local ScreenGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
ScreenGui.Name = "AimbotGUI"

local ToggleButton = Instance.new("TextButton", ScreenGui)
ToggleButton.Size = UDim2.new(0, 120, 0, 40)
ToggleButton.Position = UDim2.new(0, 10, 0, 10)
ToggleButton.Text = "Aimbot: OFF"
ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
ToggleButton.TextScaled = true

-- Variáveis
local AimbotEnabled = false

ToggleButton.MouseButton1Click:Connect(function()
	AimbotEnabled = not AimbotEnabled
	ToggleButton.Text = AimbotEnabled and "Aimbot: ON" or "Aimbot: OFF"
	ToggleButton.BackgroundColor3 = AimbotEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 0, 0)
end)

-- Função: verificar visibilidade com Raycast
local function IsVisible(part)
	local origin = Camera.CFrame.Position
	local direction = (part.Position - origin)
	
	local raycastParams = RaycastParams.new()
	raycastParams.FilterType = Enum.RaycastFilterType.Blacklist
	raycastParams.IgnoreWater = true
	raycastParams.FilterDescendantsInstances = {LocalPlayer.Character}

	local result = Workspace:Raycast(origin, direction, raycastParams)

	return not result or result.Instance:IsDescendantOf(part.Parent)
end

-- Função: obter inimigo mais próximo visível
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

-- Aimbot Loop
RunService.RenderStepped:Connect(function()
	if AimbotEnabled then
		local target = GetClosestVisiblePlayer()
		if target and target.Character and target.Character:FindFirstChild("Head") then
			local headPosition = target.Character.Head.Position
			local newLookVector = (headPosition - Camera.CFrame.Position).Unit
			Camera.CFrame = CFrame.new(Camera.CFrame.Position, Camera.CFrame.Position + newLookVector)
		end
	end
end)
