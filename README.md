# Gusta-Level
-- Gusta Level - Pegador de Frutas Automático
-- Feito por GustSCRIPTS

--// Variáveis iniciais
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local fruitStorage = game:GetService("ReplicatedStorage"):FindFirstChild("FruitStorage") -- Ajusta conforme necessário

--// Função para voar suavemente até um ponto
local function flyTo(targetPosition)
    local speed = 75 -- Ajusta a velocidade do voo
    while (humanoidRootPart.Position - targetPosition).Magnitude > 5 do
        humanoidRootPart.CFrame = humanoidRootPart.CFrame:Lerp(CFrame.new(targetPosition), 0.1)
        task.wait(0.05)
    end
end

--// Função para verificar se há espaço no inventário
local function hasInventorySpace()
    local maxFruits = 10 -- Ajusta conforme o limite do inventário
    local fruitCount = #player.Backpack:GetChildren() -- Conta as frutas no inventário
    return fruitCount < maxFruits
end

--// Função para pegar e guardar frutas
local function collectAndStoreFruits()
    for _, fruit in pairs(workspace:GetChildren()) do
        if fruit:IsA("Tool") and fruit.Name:match("Fruit") then
            print("Fruta encontrada: " .. fruit.Name)
            flyTo(fruit.Position) -- Voa até a fruta
            task.wait(1)
            firetouchinterest(humanoidRootPart, fruit.Handle, 0) -- Simula o toque na
