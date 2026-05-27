-- Referências Principais
local Player = game.Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

-- Criando a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "LevelManagerUI"
ScreenGui.Parent = PlayerGui
ScreenGui.ResetOnSpawn = false

-- Criando o Frame Principal (Janela)
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 250, 0, 150)
MainFrame.Position = UDim2.new(0.5, -125, 0.5, -75)
MainFrame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true -- Permite arrastar a janela
MainFrame.Parent = ScreenGui

-- Título
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Text = "Level Adder"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Title.Parent = MainFrame

-- Campo de Texto (Input)
local LevelInput = Instance.new("TextBox")
LevelInput.Size = UDim2.new(0.8, 0, 0, 40)
LevelInput.Position = UDim2.new(0.1, 0, 0.35, 0)
LevelInput.PlaceholderText = "Quantidade de Level..."
LevelInput.Text = ""
LevelInput.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
LevelInput.TextColor3 = Color3.fromRGB(255, 255, 255)
LevelInput.Parent = MainFrame

-- Botão de Enter
local EnterBtn = Instance.new("TextButton")
EnterBtn.Size = UDim2.new(0.8, 0, 0, 35)
EnterBtn.Position = UDim2.new(0.1, 0, 0.7, 0)
EnterBtn.Text = "Adicionar Level"
EnterBtn.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
EnterBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
EnterBtn.Parent = MainFrame

-- Lógica do Botão
EnterBtn.MouseButton1Click:Connect(function()
    local quantidade = tonumber(LevelInput.Text)
    
    if quantidade then
        print("Tentando adicionar " .. quantidade .. " levels...")
        
        -- AVISO: A linha abaixo é apenas um exemplo. 
        -- Na maioria dos jogos, mudar o valor aqui NÃO salva no servidor.
        local leaderstats = Player:FindFirstChild("leaderstats")
        if leaderstats then
            local levelValue = leaderstats:FindFirstChild("Level") or leaderstats:FindFirstChild("Leveling")
            if levelValue then
                -- Isso altera apenas visualmente no seu cliente
                levelValue.Value = levelValue.Value + quantidade
                warn("Sucesso visual! Note que o servidor pode não validar isso.")
            else
                warn("Valor 'Level' não encontrado no leaderstats.")
            end
        else
            warn("Pasta 'leaderstats' não encontrada.")
        end
    else
        warn("Por favor, digite um número válido.")
    end
end)
