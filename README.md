Implement a Lua script for Blox Fruit that adds an aimbot feature. The script should automatically aim towards the nearest enemy player when the left mouse button is held down. Ensure that the aimbot does not lock onto allied players during the aiming process. 

## Detailed Requirements: 
- Use the game's player detection system to identify enemy players. 
- Calculate the distance between the local player and all visible enemy players to determine which one is the closest. 
- Continuously update the aim direction towards the nearest enemy as long as the left mouse button remains pressed. 
- Ensure that the aimbot specifically ignores allied players, focusing only on enemies.   
- The script should be efficient and not cause noticeable lag or performance issues. 

## Steps to Implement: 
1. **Player Detection:** Use the game's API to get a list of all players and determine their team affiliation. 
2. **Distance Calculation:** Create a function to calculate the distance from the local player to each enemy player. 
3. **Aiming Logic:** Implement a mouse event listener that detects when the left mouse button is pressed and released. If pressed, trigger the aimbot to aim towards the nearest enemy. 
4. **Aim Adjustment:** Continuously adjust the player's aim towards the enemy until the button is released. 
5. **Safety Checks:** Ensure the script checks for and avoids targeting allies. 

## Output Format: 
The final output should be a complete Lua script that fulfills the above requirements, well-commented for clarity, and organized for easy understanding and editing.

## Example: 
```lua
-- Aimbot script for Blox Fruit
local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

function getClosestEnemy()
    local closestEnemy = nil
    local minDistance = math.huge
    for _, enemy in ipairs(game.Players:GetPlayers()) do
        if enemy ~= player and not enemy.Neutral then
            local distance = (player.Character.HumanoidRootPart.Position - enemy.Character.HumanoidRootPart.Position).magnitude
            if distance < minDistance then
                closestEnemy = enemy
                minDistance = distance
            end
        end
    end
    return closestEnemy
end

mouse.Button1Down:Connect(function()
    while mouse.Button1Down do
        local targetEnemy = getClosestEnemy()
        if targetEnemy then
            -- Aim at the enemy
            workspace.CurrentCamera.CFrame = CFrame.new(workspace.CurrentCamera.CFrame.Position, targetEnemy.Character.HumanoidRootPart.Position)
        end
        wait() -- Delay to avoid performance issues
    end
end)
```
## Notes: 
- Ensure to test the script in various scenarios to confirm it works as intended without errors. 
- Be aware of any game rules regarding the use of such scripts, as it can lead to penalties in some gaming environments.
