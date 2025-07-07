-- Aimbot
if AimbotEnabled then
	local maxDistance = 10
	local target = GetClosestVisiblePlayer(maxDistance)

	if target and target.Character and target.Character:FindFirstChild("Head") then
		local headPos = target.Character.Head.Position
		local look = (headPos - Camera.CFrame.Position).Unit
		Camera.CFrame = CFrame.new(Camera.CFrame.Position, Camera.CFrame.Position + look)

		-- Tiro automático (caso tenha uma Tool equipada)
		local tool = LocalPlayer.Character:FindFirstChildOfClass("Tool")
		if tool and tool:FindFirstChild("Activate") then
			tool:Activate()
		end
	end
end
