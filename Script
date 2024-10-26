local npc = script.Parent
local humanoid = npc:WaitForChild("Humanoid")
local humanoidRootPart = npc:WaitForChild("HumanoidRootPart")

local Players = game:GetService("Players")

local chaseSpeed = 16  -- Set the speed at which the NPC chases the player
local chaseInterval = 0.1  -- Time between each movement update

-- Kill player when NPC touches them
local function onTouch(hit)
	local character = hit.Parent
	local player = Players:GetPlayerFromCharacter(character)

	if player then
		local playerHumanoid = character:FindFirstChild("Humanoid")
		if playerHumanoid then
			playerHumanoid.Health = 0  -- Kill the player by setting their health to 0
		end
	end
end

-- Connect Touched event to NPC's HumanoidRootPart
humanoidRootPart.Touched:Connect(onTouch)

-- Function to make NPC chase the nearest player
local function chasePlayer()
	while true do
		local nearestPlayer = nil
		local shortestDistance = math.huge

		-- Find the closest player
		for _, player in pairs(Players:GetPlayers()) do
			local character = player.Character
			if character and character:FindFirstChild("HumanoidRootPart") then
				local playerRootPart = character.HumanoidRootPart
				local distance = (humanoidRootPart.Position - playerRootPart.Position).Magnitude
				if distance < shortestDistance then
					shortestDistance = distance
					nearestPlayer = player
				end
			end
		end

		-- If a player is found, move towards them
		if nearestPlayer and nearestPlayer.Character and nearestPlayer.Character:FindFirstChild("HumanoidRootPart") then
			local targetPosition = nearestPlayer.Character.HumanoidRootPart.Position

			-- Calculate the direction to the player
			local direction = (targetPosition - humanoidRootPart.Position).unit

			-- Move NPC towards the player
			humanoidRootPart.CFrame = humanoidRootPart.CFrame + direction * chaseSpeed * chaseInterval
		end

		wait(chaseInterval)  -- Update every 0.1 seconds (chaseInterval)
	end
end

-- Start chasing the player
chasePlayer()
