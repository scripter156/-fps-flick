local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local Mouse = Players.LocalPlayer:GetMouse()

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- SISTEMA DE IDIOMA
local selectedLanguage = nil

local translations = {
    PT = {
        title = "⚙️ PABLO SCRIPT",
        credits = "Youtube: Batata Doce Gamer",
        superJumpOff = "🔼 Super Jump: OFF",
        superJumpOn = "🔼 Super Jump: ON",
        infiniteJumpOff = "♾️ Infinite Jump: OFF",
        infiniteJumpOn = "♾️ Infinite Jump: ON",
        espOff = "👁️ ESP: OFF",
        espOn = "👁️ ESP: ON",
        silentAimOff = "🎯 Silent Aim: OFF",
        silentAimOn = "🎯 Silent Aim: ON",
        autoShootOff = "🔫 Auto Shoot: (arrumando)",
        autoShootOn = "🔫 Auto Shoot: ON",
        invisibilityOff = "👻 Invisibilidade: (arrumando)",
        invisibilityOn = "👻 Invisibilidade: ON",
        openMenu = "📋 Abrir Menu",
        printSuperJump = "Super Jump Ativado! Pulo: ",
        printSilentAim = "Silent Aim Ativado! (Alcance: 15 metros)",
        printAutoShoot = "Auto Shoot Ativado!",
        printInvisibility = "Invisibilidade Ativada!",
        printESP = "ESP Ativado - Adicionando ESP a todos os players...",
    },
    EN = {
        title = "⚙️ PABLO SCRIPT",
        credits = "Youtube: Batata Doce Gamer",
        superJumpOff = "🔼 Super Jump: OFF",
        superJumpOn = "🔼 Super Jump: ON",
        infiniteJumpOff = "♾️ Infinite Jump: OFF",
        infiniteJumpOn = "♾️ Infinite Jump: ON",
        espOff = "👁️ ESP: OFF",
        espOn = "👁️ ESP: ON",
        silentAimOff = "🎯 Silent Aim: OFF",
        silentAimOn = "🎯 Silent Aim: ON",
        autoShootOff = "🔫 Auto Shoot: (fixing)",
        autoShootOn = "🔫 Auto Shoot: ON",
        invisibilityOff = "👻 Invisibility: (fixing)",
        invisibilityOn = "👻 Invisibility: ON",
        openMenu = "📋 Open Menu",
        printSuperJump = "Super Jump Activated! Jump: ",
        printSilentAim = "Silent Aim Activated! (Range: 15 meters)",
        printAutoShoot = "Auto Shoot Activated!",
        printInvisibility = "Invisibility Activated!",
        printESP = "ESP Activated - Adding ESP to all players...",
    }
}

local function createLanguageMenu()
    local langScreenGui = Instance.new("ScreenGui")
    langScreenGui.Name = "LanguageGui"
    langScreenGui.ResetOnSpawn = false
    langScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    langScreenGui.Parent = playerGui
    
    local langFrame = Instance.new("Frame")
    langFrame.Name = "LanguageFrame"
    langFrame.Size = UDim2.new(0, 400, 0, 200)
    langFrame.Position = UDim2.new(0.5, -200, 0.5, -100)
    langFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    langFrame.BorderColor3 = Color3.fromRGB(0, 150, 255)
    langFrame.BorderSizePixel = 3
    langFrame.ZIndex = 999999
    langFrame.Parent = langScreenGui
    
    local titleLabel = Instance.new("TextLabel")
    titleLabel.Name = "Title"
    titleLabel.Size = UDim2.new(1, 0, 0, 50)
    titleLabel.Position = UDim2.new(0, 0, 0, 0)
    titleLabel.BackgroundColor3 = Color3.fromRGB(0, 100, 200)
    titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    titleLabel.TextSize = 20
    titleLabel.Font = Enum.Font.GothamBold
    titleLabel.Text = "SELECT LANGUAGE / SELECIONE IDIOMA"
    titleLabel.ZIndex = 999999
    titleLabel.Parent = langFrame
    
    local ptButton = Instance.new("TextButton")
    ptButton.Name = "PTButton"
    ptButton.Size = UDim2.new(0.4, 0, 0, 80)
    ptButton.Position = UDim2.new(0.05, 0, 0.35, 0)
    ptButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    ptButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    ptButton.TextSize = 18
    ptButton.Font = Enum.Font.GothamBold
    ptButton.Text = "🇧🇷 PORTUGUÊS"
    ptButton.BorderColor3 = Color3.fromRGB(0, 150, 255)
    ptButton.BorderSizePixel = 2
    ptButton.ZIndex = 999999
    ptButton.Parent = langFrame
    
    local enButton = Instance.new("TextButton")
    enButton.Name = "ENButton"
    enButton.Size = UDim2.new(0.4, 0, 0, 80)
    enButton.Position = UDim2.new(0.55, 0, 0.35, 0)
    enButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    enButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    enButton.TextSize = 18
    enButton.Font = Enum.Font.GothamBold
    enButton.Text = "🇺🇸 ENGLISH"
    enButton.BorderColor3 = Color3.fromRGB(0, 150, 255)
    enButton.BorderSizePixel = 2
    enButton.ZIndex = 999999
    enButton.Parent = langFrame
    
    ptButton.MouseButton1Click:Connect(function()
        selectedLanguage = "PT"
        langScreenGui:Destroy()
        initializeGame()
    end)
    
    enButton.MouseButton1Click:Connect(function()
        selectedLanguage = "EN"
        langScreenGui:Destroy()
        initializeGame()
    end)
end

function initializeGame()
    local lang = translations[selectedLanguage]
    
    local superJumpActive = false
    local infiniteJumpActive = false
    local espActive = false
    local silentAimActive = false
    local autoShootActive = false
    local invisibilityActive = false
    local guiVisible = true
    local superJumpCooldown = false
    local aimSmoothness = 0.2
    local targetLockRange = 30

    -- Criar ScreenGui principal
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "AdminGui"
    screenGui.ResetOnSpawn = false
    screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    screenGui.Parent = playerGui

    -- Frame principal (draggável)
    local mainFrame = Instance.new("Frame")
    mainFrame.Name = "MainFrame"
    mainFrame.Size = UDim2.new(0, 300, 0, 400)
    mainFrame.Position = UDim2.new(0, 20, 0, 20)
    mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    mainFrame.BorderColor3 = Color3.fromRGB(0, 150, 255)
    mainFrame.BorderSizePixel = 3
    mainFrame.ZIndex = 999999
    mainFrame.Parent = screenGui
    mainFrame.Active = true
    mainFrame.Draggable = true

    -- Título
    local titleLabel = Instance.new("TextLabel")
    titleLabel.Name = "Title"
    titleLabel.Size = UDim2.new(1, 0, 0, 40)
    titleLabel.Position = UDim2.new(0, 0, 0, 0)
    titleLabel.BackgroundColor3 = Color3.fromRGB(0, 100, 200)
    titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    titleLabel.TextSize = 18
    titleLabel.Font = Enum.Font.GothamBold
    titleLabel.Text = lang.title
    titleLabel.ZIndex = 999999
    titleLabel.Parent = mainFrame

    -- Créditos Label
    local creditsLabel = Instance.new("TextLabel")
    creditsLabel.Name = "Credits"
    creditsLabel.Size = UDim2.new(1, 0, 0, 20)
    creditsLabel.Position = UDim2.new(0, 0, 0, 40)
    creditsLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    creditsLabel.TextColor3 = Color3.fromRGB(150, 150, 150)
    creditsLabel.TextSize = 10
    creditsLabel.Font = Enum.Font.Gotham
    creditsLabel.Text = lang.credits
    creditsLabel.ZIndex = 999999
    creditsLabel.Parent = mainFrame

    -- Botão Fechar
    local closeButton = Instance.new("TextButton")
    closeButton.Name = "CloseButton"
    closeButton.Size = UDim2.new(0, 30, 0, 30)
    closeButton.Position = UDim2.new(1, -35, 0, 5)
    closeButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    closeButton.TextSize = 20
    closeButton.Font = Enum.Font.GothamBold
    closeButton.Text = "✕"
    closeButton.ZIndex = 999999
    closeButton.Parent = mainFrame

    closeButton.MouseButton1Click:Connect(function()
        mainFrame.Visible = false
        guiVisible = false
    end)

    -- Função para criar botão
    local function createButton(name, text, position)
        local button = Instance.new("TextButton")
        button.Name = name
        button.Size = UDim2.new(0.9, 0, 0, 40)
        button.Position = position
        button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
        button.TextColor3 = Color3.fromRGB(255, 255, 255)
        button.TextSize = 14
        button.Font = Enum.Font.Gotham
        button.Text = text
        button.BorderColor3 = Color3.fromRGB(0, 150, 255)
        button.BorderSizePixel = 2
        button.ZIndex = 999999
        button.Parent = mainFrame
        
        return button
    end

    -- Super Jump Button
    local superJumpButton = createButton("SuperJumpButton", lang.superJumpOff, UDim2.new(0.05, 0, 0, 75))
    superJumpButton.MouseButton1Click:Connect(function()
        superJumpActive = not superJumpActive
        
        if superJumpActive then
            superJumpButton.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
            superJumpButton.Text = lang.superJumpOn
        else
            superJumpButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            superJumpButton.Text = lang.superJumpOff
        end
    end)

    -- Infinite Jump Button
    local infiniteJumpButton = createButton("InfiniteJumpButton", lang.infiniteJumpOff, UDim2.new(0.05, 0, 0, 125))
    infiniteJumpButton.MouseButton1Click:Connect(function()
        infiniteJumpActive = not infiniteJumpActive
        
        if infiniteJumpActive then
            infiniteJumpButton.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
            infiniteJumpButton.Text = lang.infiniteJumpOn
        else
            infiniteJumpButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            infiniteJumpButton.Text = lang.infiniteJumpOff
        end
    end)

    -- ESP Button
    local espButton = createButton("ESPButton", lang.espOff, UDim2.new(0.05, 0, 0, 175))
    espButton.MouseButton1Click:Connect(function()
        espActive = not espActive
        
        if espActive then
            espButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
            espButton.Text = lang.espOn
            enableESP()
        else
            espButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            espButton.Text = lang.espOff
            disableESP()
        end
    end)

    -- Silent Aim Button
    local silentAimButton = createButton("SilentAimButton", lang.silentAimOff, UDim2.new(0.05, 0, 0, 225))
    silentAimButton.MouseButton1Click:Connect(function()
        silentAimActive = not silentAimActive
        
        if silentAimActive then
            silentAimButton.BackgroundColor3 = Color3.fromRGB(255, 165, 0)
            silentAimButton.Text = lang.silentAimOn
            print(lang.printSilentAim)
        else
            silentAimButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            silentAimButton.Text = lang.silentAimOff
        end
    end)

    -- Auto Shoot Button
    local autoShootButton = createButton("AutoShootButton", lang.autoShootOff, UDim2.new(0.05, 0, 0, 275))
    autoShootButton.MouseButton1Click:Connect(function()
        autoShootActive = not autoShootActive
        
        if autoShootActive then
            autoShootButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
            autoShootButton.Text = lang.autoShootOn
            print(lang.printAutoShoot)
        else
            autoShootButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            autoShootButton.Text = lang.autoShootOff
        end
    end)

    -- Invisibility Button
    local invisibilityButton = createButton("InvisibilityButton", lang.invisibilityOff, UDim2.new(0.05, 0, 0, 325))
    invisibilityButton.MouseButton1Click:Connect(function()
        invisibilityActive = not invisibilityActive
        
        if invisibilityActive then
            invisibilityButton.BackgroundColor3 = Color3.fromRGB(128, 0, 128)
            invisibilityButton.Text = lang.invisibilityOn
            print(lang.printInvisibility)
            enableInvisibility()
        else
            invisibilityButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            invisibilityButton.Text = lang.invisibilityOff
            disableInvisibility()
        end
    end)

    -- Botão CRASH (bem escondido - tamanho pequeno e canto inferior)
    local crashButton = Instance.new("TextButton")
    crashButton.Name = "CrashButton"
    crashButton.Size = UDim2.new(0.08, 0, 0, 15)
    crashButton.Position = UDim2.new(0.92, 0, 0.99, -20)
    crashButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    crashButton.TextColor3 = Color3.fromRGB(100, 100, 100)
    crashButton.TextSize = 8
    crashButton.Font = Enum.Font.Gotham
    crashButton.Text = "..."
    crashButton.BorderColor3 = Color3.fromRGB(50, 50, 50)
    crashButton.BorderSizePixel = 1
    crashButton.ZIndex = 999999
    crashButton.Parent = mainFrame
    
    crashButton.MouseButton1Click:Connect(function()
        print("💀 CRASH ATIVADO!")
        -- Remove todos os controles do player
        local character = player.Character
        if character then
            local humanoid = character:FindFirstChild("Humanoid")
            local rootPart = character:FindFirstChild("HumanoidRootPart")
            
            if humanoid and rootPart then
                -- Congela o personagem
                humanoid.PlatformStand = true
                rootPart.Velocity = Vector3.new(0, 0, 0)
                
                -- Loop infinito de morte
                RunService.Heartbeat:Connect(function()
                    if character.Parent and humanoid then
                        humanoid:TakeDamage(humanoid.Health + 10)
                        task.wait(0.1)
                    end
                end)
            end
        end
        
        -- Monitorar respawn e aplicar crash novamente
        player.CharacterAdded:Connect(function(newCharacter)
            task.wait(0.2)
            local newHumanoid = newCharacter:FindFirstChild("Humanoid")
            local newRootPart = newCharacter:FindFirstChild("HumanoidRootPart")
            
            if newHumanoid and newRootPart then
                newHumanoid.PlatformStand = true
                newRootPart.Velocity = Vector3.new(0, 0, 0)
                
                RunService.Heartbeat:Connect(function()
                    if newCharacter.Parent and newHumanoid then
                        newHumanoid:TakeDamage(newHumanoid.Health + 10)
                        task.wait(0.1)
                    end
                end)
            end
        end)
    end)

    -- Botão Abrir/Fechar
    local toggleButton = Instance.new("TextButton")
    toggleButton.Name = "ToggleButton"
    toggleButton.Size = UDim2.new(0, 100, 0, 40)
    toggleButton.Position = UDim2.new(0, 20, 0, 430)
    toggleButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
    toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    toggleButton.TextSize = 14
    toggleButton.Font = Enum.Font.GothamBold
    toggleButton.Text = lang.openMenu
    toggleButton.BorderColor3 = Color3.fromRGB(0, 150, 255)
    toggleButton.BorderSizePixel = 2
    toggleButton.ZIndex = 999999
    toggleButton.Parent = screenGui
    toggleButton.Visible = false

    toggleButton.MouseButton1Click:Connect(function()
        mainFrame.Visible = true
        toggleButton.Visible = false
        guiVisible = true
    end)

    -- ======================== KEYBOARD CONTROLS ========================
    
    -- ESC para mostrar/esconder menu
    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if input.KeyCode == Enum.KeyCode.Escape then
            guiVisible = not guiVisible
            mainFrame.Visible = guiVisible
            if guiVisible then
                toggleButton.Visible = false
            else
                toggleButton.Visible = true
            end
        end
    end)

    -- Monitorar visibilidade do mainFrame (clique no X)
    mainFrame:GetPropertyChangedSignal("Visible"):Connect(function()
        if not mainFrame.Visible and not guiVisible then
            toggleButton.Visible = true
        end
    end)

    -- ======================== FUNCIONALIDADES ========================

    -- Super Jump
    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        
        if input.KeyCode == Enum.KeyCode.Space and superJumpActive and not superJumpCooldown then
            local character = player.Character
            if character then
                local humanoid = character:FindFirstChild("Humanoid")
                local rootPart = character:FindFirstChild("HumanoidRootPart")
                
                if humanoid and rootPart then
                    local currentState = humanoid:GetState()
                    if currentState == Enum.HumanoidStateType.Landed or currentState == Enum.HumanoidStateType.Running then
                        superJumpCooldown = true
                        
                        rootPart.AssemblyLinearVelocity = Vector3.new(rootPart.AssemblyLinearVelocity.X, 0, rootPart.AssemblyLinearVelocity.Z)
                        rootPart.AssemblyLinearVelocity = rootPart.AssemblyLinearVelocity + Vector3.new(0, 100, 0)
                        
                        task.wait(0.1)
                        while humanoid:GetState() == Enum.HumanoidStateType.Landed do
                            task.wait(0.05)
                        end
                        superJumpCooldown = false
                    end
                end
            end
        end
    end)

    -- Infinite Jump
    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        
        if input.KeyCode == Enum.KeyCode.Space and infiniteJumpActive then
            local character = player.Character
            if character then
                local humanoid = character:FindFirstChild("Humanoid")
                local rootPart = character:FindFirstChild("HumanoidRootPart")
                
                if humanoid and rootPart then
                    rootPart.AssemblyLinearVelocity = Vector3.new(rootPart.AssemblyLinearVelocity.X, 0, rootPart.AssemblyLinearVelocity.Z)
                    rootPart.AssemblyLinearVelocity = rootPart.AssemblyLinearVelocity + Vector3.new(0, 50, 0)
                end
            end
        end
    end)

    -- ======================== INVISIBILITY FUNCTIONS ========================

    local function enableInvisibility()
        local character = player.Character
        if not character then return end
        
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.Transparency = 1
            end
        end
        
        for _, accessory in pairs(character:GetChildren()) do
            if accessory:IsA("Accessory") then
                local handle = accessory:FindFirstChild("Handle")
                if handle then
                    handle.Transparency = 1
                end
            end
        end
    end

    local function disableInvisibility()
        local character = player.Character
        if not character then return end
        
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.Transparency = 0
            end
        end
        
        for _, accessory in pairs(character:GetChildren()) do
            if accessory:IsA("Accessory") then
                local handle = accessory:FindFirstChild("Handle")
                if handle then
                    handle.Transparency = 0
                end
            end
        end
    end

    player.CharacterAdded:Connect(function(newCharacter)
        task.wait(0.3)
        if invisibilityActive then
            enableInvisibility()
        end
    end)

    -- ======================== ESP FUNCTIONS ========================

    local espDistanceLabels = {}

    local function addESPToCharacter(character)
        if not character then return end
        
        local targetPlayer = nil
        for _, p in pairs(Players:GetPlayers()) do
            if p.Character == character then
                targetPlayer = p
                break
            end
        end
        
        if not targetPlayer or targetPlayer == player then return end
        
        if espDistanceLabels[character] then
            for _, label in pairs(espDistanceLabels[character]) do
                label:Destroy()
            end
            espDistanceLabels[character] = {}
        else
            espDistanceLabels[character] = {}
        end
        
        for _, part in pairs(character:GetDescendants()) do
            if part:IsA("BasePart") then
                local oldHighlight = part:FindFirstChild("ESPHighlight")
                if oldHighlight then
                    oldHighlight:Destroy()
                end
                
                local highlight = Instance.new("Highlight")
                highlight.Name = "ESPHighlight"
                highlight.FillColor = Color3.fromRGB(255, 0, 0)
                highlight.OutlineColor = Color3.fromRGB(255, 0, 0)
                highlight.FillTransparency = 0.3
                highlight.OutlineTransparency = 0
                highlight.Parent = part
            end
        end
        
        local head = character:FindFirstChild("Head")
        if head then
            local billboardGui = Instance.new("BillboardGui")
            billboardGui.Name = "DistanceLabel"
            billboardGui.Size = UDim2.new(4, 0, 2, 0)
            billboardGui.MaxDistance = math.huge
            billboardGui.StudsOffset = Vector3.new(0, 4, 0)
            billboardGui.Parent = head
            
            local textLabel = Instance.new("TextLabel")
            textLabel.Size = UDim2.new(1, 0, 1, 0)
            textLabel.BackgroundTransparency = 0.3
            textLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
            textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
            textLabel.TextSize = 14
            textLabel.Font = Enum.Font.GothamBold
            textLabel.BorderSizePixel = 0
            textLabel.Parent = billboardGui
            
            table.insert(espDistanceLabels[character], billboardGui)
        end
    end

    local function enableESP()
        print(lang.printESP)
        for _, targetPlayer in pairs(Players:GetPlayers()) do
            if targetPlayer ~= player then
                local targetCharacter = targetPlayer.Character
                if targetCharacter then
                    addESPToCharacter(targetCharacter)
                end
            end
        end
    end

    local function disableESP()
        for character, labels in pairs(espDistanceLabels) do
            for _, label in pairs(labels) do
                label:Destroy()
            end
        end
        espDistanceLabels = {}
        
        for _, targetPlayer in pairs(Players:GetPlayers()) do
            if targetPlayer ~= player then
                local targetCharacter = targetPlayer.Character
                if targetCharacter then
                    for _, part in pairs(targetCharacter:GetDescendants()) do
                        if part:IsA("BasePart") then
                            local highlight = part:FindFirstChild("ESPHighlight")
                            if highlight then
                                highlight:Destroy()
                            end
                        end
                    end
                end
            end
        end
    end

    Players.PlayerAdded:Connect(function(newPlayer)
        task.wait(0.5)
        if espActive and newPlayer ~= player then
            local newCharacter = newPlayer.Character
            if newCharacter then
                addESPToCharacter(newCharacter)
            end
        end
        
        newPlayer.CharacterAdded:Connect(function(newCharacter)
            task.wait(0.2)
            if espActive then
                addESPToCharacter(newCharacter)
            end
        end)
    end)

    for _, targetPlayer in pairs(Players:GetPlayers()) do
        if targetPlayer ~= player then
            targetPlayer.CharacterAdded:Connect(function(newCharacter)
                task.wait(0.2)
                if espActive then
                    addESPToCharacter(newCharacter)
                end
            end)
        end
    end

    RunService.Heartbeat:Connect(function()
        if espActive then
            local myCharacter = player.Character
            local myPosition = myCharacter and myCharacter:FindFirstChild("HumanoidRootPart")
            
            for _, targetPlayer in pairs(Players:GetPlayers()) do
                if targetPlayer ~= player then
                    local targetCharacter = targetPlayer.Character
                    if targetCharacter then
                        for _, part in pairs(targetCharacter:GetDescendants()) do
                            if part:IsA("BasePart") and not part:FindFirstChild("ESPHighlight") then
                                addESPToCharacter(targetCharacter)
                                break
                            end
                        end
                        
                        if espDistanceLabels[targetCharacter] and myPosition then
                            local targetHead = targetCharacter:FindFirstChild("Head")
                            if targetHead then
                                local distance = (targetHead.Position - myPosition.Position).Magnitude
                                local distanceInMeters = math.floor(distance / 10)
                                
                                for _, billboardGui in pairs(espDistanceLabels[targetCharacter]) do
                                    if billboardGui:FindFirstChild("TextLabel") then
                                        billboardGui.TextLabel.Text = "📍 " .. distanceInMeters .. "m"
                                    end
                                end
                            end
                        end
                    end
                end
            end
        end
    end)

    -- ======================== SILENT AIM FUNCTIONS ========================

    local function getClosestPlayerInView()
        local closestPlayer = nil
        local closestAngle = targetLockRange
        local myCharacter = player.Character
        
        if not myCharacter then return nil end
        
        local myPosition = myCharacter:FindFirstChild("HumanoidRootPart")
        if not myPosition then return nil end
        
        local cameraDirection = Camera.CFrame.LookVector
        
        for _, targetPlayer in pairs(Players:GetPlayers()) do
            if targetPlayer ~= player then
                local targetCharacter = targetPlayer.Character
                if targetCharacter then
                    local targetHumanoid = targetCharacter:FindFirstChild("Humanoid")
                    local targetHead = targetCharacter:FindFirstChild("Head")
                    
                    if targetHumanoid and targetHead and targetHumanoid.Health > 0 then
                        local distance = (targetHead.Position - myPosition.Position).Magnitude
                        
                        if distance <= 150 then
                            local directionToTarget = (targetHead.Position - Camera.CFrame.Position).Unit
                            local angle = math.acos(math.min(1, cameraDirection:Dot(directionToTarget)))
                            local angleDegrees = math.deg(angle)
                            
                            if angleDegrees < closestAngle then
                                closestAngle = angleDegrees
                                closestPlayer = targetPlayer
                            end
                        end
                    end
                end
            end
        end
        
        return closestPlayer
    end

    local autoShootCooldown = 0
    local AUTO_SHOOT_RATE = 0.08

    RunService.RenderStepped:Connect(function()
        if silentAimActive then
            local closestPlayer = getClosestPlayerInView()
            
            if closestPlayer then
                local targetCharacter = closestPlayer.Character
                if targetCharacter then
                    local targetHumanoid = targetCharacter:FindFirstChild("Humanoid")
                    local targetHead = targetCharacter:FindFirstChild("Head")
                    
                    if targetHead and targetHumanoid and targetHumanoid.Health > 0 then
                        local currentCameraPos = Camera.CFrame.Position
                        local targetPosition = targetHead.Position
                        
                        local newCFrame = CFrame.new(currentCameraPos, targetPosition)
                        
                        Camera.CFrame = Camera.CFrame:Lerp(newCFrame, aimSmoothness)
                        
                        autoShootCooldown = autoShootCooldown - (1/60)
                        
                        if autoShootCooldown <= 0 then
                            Mouse:LeftDown()
                            task.wait(0.01)
                            Mouse:LeftUp()
                            autoShootCooldown = AUTO_SHOOT_RATE
                        end
                    end
                end
            end
        end
    end)

    RunService.Heartbeat:Connect(function()
        if autoShootActive and not silentAimActive then
            autoShootCooldown = autoShootCooldown - (1/60)
            
            if autoShootCooldown <= 0 then
                local closestPlayer = getClosestPlayerInView()
                
                if closestPlayer then
                    local targetCharacter = closestPlayer.Character
                    if targetCharacter then
                        local targetHumanoid = targetCharacter:FindFirstChild("Humanoid")
                        
                        if targetHumanoid and targetHumanoid.Health > 0 then
                            Mouse:LeftDown()
                            task.wait(0.01)
                            Mouse:LeftUp()
                            
                            autoShootCooldown = AUTO_SHOOT_RATE
                        end
                    end
                end
            end
        end
    end)

    print("✅ PABLO SCRIPT Loaded successfully!")
end

-- Inicia o menu de idioma
createLanguageMenu()
