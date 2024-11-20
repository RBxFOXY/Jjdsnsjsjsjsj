-- Definindo a função para encontrar a fruta mais próxima
local function findNearestFruit()
    local fruits = game.Workspace.Fruits:GetChildren()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local closestFruit = nil
    local shortestDistance = math.huge

    for _, fruit in pairs(fruits) do
        if fruit and fruit.Position then
            local distance = (fruit.Position - character.HumanoidRootPart.Position).magnitude
            if distance < shortestDistance then
                closestFruit = fruit
                shortestDistance = distance
            end
        end
    end

    return closestFruit
end

-- Função para teleportar o jogador até a fruta
local function teleportToFruit(fruit)
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    if fruit and character and character.HumanoidRootPart then
        character.HumanoidRootPart.CFrame = fruit.CFrame
    end
end

-- Loop para verificar e pegar frutas automaticamente
while true do
    local fruit = findNearestFruit()
    if fruit then
        teleportToFruit(fruit)
    end
    wait(2) -- Espera 2 segundos antes de verificar novamente
end
