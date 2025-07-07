local function GetClosestVisiblePlayer(maxDistance)
	local closest = nil
	local shortest = math.huge

	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Head") then
			local head = player.Character.Head
			local screenPos, onScreen = Camera:WorldToViewportPoint(head.Position)
			local distanceToPlayer = (head.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude

			if onScreen and IsVisible(head) and distanceToPlayer <= maxDistance then
				local mouseDistance = (Vector2.new(screenPos.X, screenPos.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
				if mouseDistance < shortest then
					shortest = mouseDistance
					closest = player
				end
			end
		end
	end
	return closest
end
