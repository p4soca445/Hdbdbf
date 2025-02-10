-- Tornado básico em Roblox
local tornado = Instance.new("Part")
tornado.Shape = Enum.PartType.Ball
tornado.Size = Vector3.new(50, 50, 50)
tornado.Position = Vector3.new(0, 50, 0)  -- Posição inicial do tornado
tornado.Anchored = true
tornado.CanCollide = false
tornado.Material = Enum.Material.SmoothPlastic
tornado.Color = Color3.fromRGB(100, 100, 255)
tornado.Parent = workspace

-- Efeitos visuais (gerar partículas)
local tornadoEffect = Instance.new("ParticleEmitter")
tornadoEffect.Parent = tornado
tornadoEffect.Texture = "rbxassetid://1234567890"  -- ID de textura do efeito visual (adicione sua textura de tornado)
tornadoEffect.Size = NumberSequence.new(10, 30)
tornadoEffect.Lifetime = NumberRange.new(3, 5)
tornadoEffect.Rate = 100
tornadoEffect.Speed = NumberRange.new(10, 20)

-- Função para puxar objetos e o personagem para o tornado
game:GetService("RunService").Heartbeat:Connect(function()
    for _, object in ipairs(workspace:GetChildren()) do
        -- Só puxa objetos que têm um humanoide
        if object:IsA("Model") and object:FindFirstChildOfClass("Humanoid") then
            local humanoidRootPart = object:FindFirstChild("HumanoidRootPart")
            if humanoidRootPart then
                local direction = tornado.Position - humanoidRootPart.Position
                local force = direction.Unit * 50  -- Intensidade da atração
                humanoidRootPart.Velocity = humanoidRootPart.Velocity + force
            end
        end
    end
end)
