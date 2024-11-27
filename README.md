local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local targetMobName = "Bandit"  -- Nome do mob

local closestTarget = nil
local shortestDistance = math.huge

while true do
    for _, obj in pairs(workspace:GetChildren()) do
        if obj:IsA("Model") and obj:FindFirstChild("Humanoid") and obj.Name == targetMobName then
            local distance = (obj.HumanoidRootPart.Position - character.HumanoidRootPart.Position).Magnitude
            if distance < shortestDistance then
                closestTarget = obj
                shortestDistance = distance
            end
        end
    end

    if closestTarget then
        character:MoveTo(closestTarget.HumanoidRootPart.Position)
        wait(1)
        closestTarget.Humanoid:TakeDamage(10)
    end
    wait(0.5)
end
