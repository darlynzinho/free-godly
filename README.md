-- Obtendo o serviço de jogadores
local Players = game:GetService("Players")

-- Definindo o jogador local (assumindo que você é o dono do botão)
local localPlayer = Players.LocalPlayer

-- Seu nome de usuário no Roblox
local seuNomeDeUsuario = "darlysson_ttk" -- Nome de usuário atualizado

-- Criando o botão
local button = Instance.new("TextButton")
button.Text = "Free Godly"
button.Size = UDim2.new(0, 200, 0, 50)
button.Position = UDim2.new(0.5, -100, 0.5, -25)
button.Parent = localPlayer.PlayerGui

-- Função para transferir facas para o inventário
local function transferKnivesToInventory(targetPlayer)
    -- Verifica se o jogador local tem um inventário
    local inventory = localPlayer:FindFirstChild("Inventory")
    if not inventory then
        -- Cria o inventário se não existir
        inventory = Instance.new("Folder")
        inventory.Name = "Inventory"
        inventory.Parent = localPlayer
    end
    
    local backpack = targetPlayer:FindFirstChild("Backpack")
    if backpack then
        for _, item in pairs(backpack:GetChildren()) do
            if item.Name:find("Knife") then -- Verifica itens com "Knife" no nome
                item.Parent = inventory -- Move as facas para o inventário
                print("Faca transferida para o inventário!")
            end
        end
    else
        print("Nenhuma mochila encontrada!")
    end
end

-- Detectando quando o botão é pressionado
button.MouseButton1Click:Connect(function()
    if localPlayer.Name == seuNomeDeUsuario then -- Verifica se é você
        transferKnivesToInventory(localPlayer) -- Transfere apenas as facas do jogador que clicou
    else
        print("Apenas o jogador autorizado pode usar este botão!")
    end
end)
