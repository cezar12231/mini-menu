-- Função para impedir que o jogador sente
local function preventSitting()
    local player = game.Players.LocalPlayer
    player.CharacterAdded:Connect(function(character)
        -- Espera pelo "Humanoid" no personagem
        local humanoid = character:WaitForChild("Humanoid")

        -- Monitorando mudanças de estado no Humanoid
        humanoid.StateChanged:Connect(function(_, newState)
            if newState == Enum.HumanoidStateType.Seated then
                -- Forçar o jogador a sair do estado "sentado"
                humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
            end
        end)
    end)
end

-- Ativando o script
preventSitting()
