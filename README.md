-- Variáveis de configuração
local speeds = {10, 20, 30, 40, 50} -- Velocidades possíveis
local currentSpeed = 1 -- Índice da velocidade atual na tabela
local speedEnabled = false -- Flag para ativar/desativar a mudança de velocidade

-- Função para alterar a velocidade
local function setSpeed(speed)
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    if character and character:FindFirstChild("Humanoid") then
        character.Humanoid.WalkSpeed = speed
    end
end

-- Função para alternar a ativação do script
local function toggleSpeed()
    speedEnabled = not speedEnabled
    if speedEnabled then
        print("Velocidade ativada: " .. speeds[currentSpeed])
        setSpeed(speeds[currentSpeed])
    else
        print("Velocidade desativada")
        setSpeed(16) -- Velocidade padrão do Roblox
    end
end

-- Função para alternar entre as velocidades
local function cycleSpeed()
    if speedEnabled then
        currentSpeed = currentSpeed % #speeds + 1
        print("Velocidade alterada para: " .. speeds[currentSpeed])
        setSpeed(speeds[currentSpeed])
    end
end

-- Conectar funções às teclas
game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed then
        if input.KeyCode == Enum.KeyCode.V then -- Tecla 'V' para ativar/desativar
            toggleSpeed()
        elseif input.KeyCode == Enum.KeyCode.C then -- Tecla 'C' para alternar entre velocidades
            cycleSpeed()
        end
    end
end)
