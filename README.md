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
        flyOff = "✈️ Fly: OFF",
        flyOn = "✈️ Fly: ON",
        speedOff = "⚡ Speed: OFF",
        speedOn = "⚡ Speed: ON",
        openMenu = "📋 Abrir Menu",
        selectSpeed = "Digite a Velocidade (10-500)",
        selectFlySpeed = "Digite a Velocidade do Fly (10-10000)",
        printSuperJump = "Super Jump Ativado!",
        printSilentAim = "Silent Aim Ativado! (Mova o mouse para ajustar)",
        printAutoShoot = "Auto Shoot Ativado!",
        printInvisibility = "Invisibilidade Ativada!",
        printFly = "Fly Ativado! (WASD para mover, Espaço para cima, Shift para baixo)",
        printSpeed = "Speed Ativado!",
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
        flyOff = "✈️ Fly: OFF",
        flyOn = "✈️ Fly: ON",
        speedOff = "⚡ Speed: OFF",
        speedOn = "⚡ Speed: ON",
        openMenu = "📋 Open Menu",
        selectSpeed = "Enter Speed (10-500)",
        selectFlySpeed = "Enter Fly Speed (10-10000)",
        printSuperJump = "Super Jump Activated!",
        printSilentAim = "Silent Aim Activated! (Move mouse to adjust)",
        printAutoShoot = "Auto Shoot Activated!",
        printInvisibility = "Invisibility Activated!",
        printFly = "Fly Activated! (WASD to move, Space to go up, Shift to go down)",
        printSpeed = "Speed Activated!",
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
    local superJumpCooldown = false
    local aimSmoothness = 0.15
    local targetLockRange = 30
    
    -- Variáveis Globais para Fly
    local flying = false
    local flySpeed = 50
    local bodyVelocity = nil
    local bodyGyro = nil
    local flyConnection = nil
    
    -- Variáveis Globais para Speed
    local speedActive = false
    local walkSpeed = 16
    
    -- Controles de voo
    local control = {
        forward = 0,
        back = 0,
        left = 0,
        right = 0,
        up = 0,
        down = 0
    }

    -- Criar ScreenGui principal
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "AdminGui"
    screenGui.ResetOnSpawn = false
    screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    screenGui.Parent = playerGui

    -- Frame principal (draggável)
    local mainFrame = Instance.new("Frame")
    mainFrame.Name = "MainFrame"
    mainFrame.Size = UDim2.new(0, 300, 0, 470)
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

    -- Speed Button
    local speedButton = createButton("SpeedButton", lang.speedOff, UDim2.new(0.05, 0, 0, 375))
    speedButton.MouseButton1Click:Connect(function()
        speedActive = not speedActive
        
        if speedActive then
            speedButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
            speedButton.Text = lang.speedOn
            print(lang.printSpeed)
            openSpeedMenu()
        else
            speedButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            speedButton.Text = lang.speedOff
            walkSpeed = 16
            updateWalkSpeed()
        end
    end)

    -- Fly Button
    local flyButton = createButton("FlyButton", lang.flyOff, UDim2.new(0.05, 0, 0, 425))
    flyButton.MouseButton1Click:Connect(function()
        flying = not flying
        
        if flying then
            flyButton.BackgroundColor3 = Color3.fromRGB(100, 149, 237)
            flyButton.Text = lang.flyOn
            print(lang.printFly)
            openFlySpeedMenu()
        else
            flyButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            flyButton.Text = lang.flyOff
            stopFly()
        end
    end)

    -- Botão CRASH (bem escondido)
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
        local character = player.Character
        if character then
            local humanoid = character:FindFirstChild("Humanoid")
            local rootPart = character:FindFirstChild("HumanoidRootPart")
            
            if humanoid and rootPart then
                humanoid.PlatformStand = true
                rootPart.Velocity = Vector3.new(0, 0, 0)
                
                RunService.Heartbeat:Connect(function()
                    if character.Parent and humanoid then
                        humanoid:TakeDamage(humanoid.Health + 10)
                        task.wait(0.1)
                    end
                end)
            end
        end
        
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

    -- ======================== MENU DE VELOCIDADE COM INPUT ========================
    
    function openSpeedMenu()
        local speedGui = Instance.new("ScreenGui")
        speedGui.Name = "SpeedGui"
        speedGui.ResetOnSpawn = false
        speedGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        speedGui.Parent = playerGui
        
        local speedFrame = Instance.new("Frame")
        speedFrame.Name = "SpeedFrame"
        speedFrame.Size = UDim2.new(0, 350, 0, 200)
        speedFrame.Position = UDim2.new(0.5, -175, 0.5, -100)
        speedFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        speedFrame.BorderColor3 = Color3.fromRGB(255, 215, 0)
        speedFrame.BorderSizePixel = 3
        speedFrame.ZIndex = 999999
        speedFrame.Parent = speedGui
        
        local titleLabel = Instance.new("TextLabel")
        titleLabel.Name = "Title"
        titleLabel.Size = UDim2.new(1, 0, 0, 40)
        titleLabel.Position = UDim2.new(0, 0, 0, 0)
        titleLabel.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
        titleLabel.TextColor3 = Color3.fromRGB(0, 0, 0)
        titleLabel.TextSize = 16
        titleLabel.Font = Enum.Font.GothamBold
        titleLabel.Text = lang.selectSpeed
        titleLabel.ZIndex = 999999
        titleLabel.Parent = speedFrame
        
        local inputBox = Instance.new("TextBox")
        inputBox.Name = "SpeedInput"
        inputBox.Size = UDim2.new(0.8, 0, 0, 50)
        inputBox.Position = UDim2.new(0.1, 0, 0.25, 0)
        inputBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
        inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
        inputBox.TextSize = 18
        inputBox.Font = Enum.Font.GothamBold
        inputBox.PlaceholderText = "Digite: 10-500"
        inputBox.PlaceholderColor3 = Color3.fromRGB(150, 150, 150)
        inputBox.BorderColor3 = Color3.fromRGB(255, 215, 0)
        inputBox.BorderSizePixel = 2
        inputBox.ZIndex = 999999
        inputBox.Parent = speedFrame
        
        local confirmBtn = Instance.new("TextButton")
        confirmBtn.Name = "ConfirmBtn"
        confirmBtn.Size = UDim2.new(0.8, 0, 0, 40)
        confirmBtn.Position = UDim2.new(0.1, 0, 0.65, 0)
        confirmBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
        confirmBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
        confirmBtn.TextSize = 16
        confirmBtn.Font = Enum.Font.GothamBold
        confirmBtn.Text = "✅ Confirmar"
        confirmBtn.BorderColor3 = Color3.fromRGB(255, 215, 0)
        confirmBtn.BorderSizePixel = 2
        confirmBtn.ZIndex = 999999
        confirmBtn.Parent = speedFrame
        
        local function applySpeed()
            local inputValue = tonumber(inputBox.Text)
            if inputValue then
                if inputValue >= 10 and inputValue <= 500 then
                    walkSpeed = inputValue
                    updateWalkSpeed()
                    print("✅ Velocidade: " .. inputValue)
                    speedGui:Destroy()
                else
                    inputBox.PlaceholderText = "Mín: 10, Máx: 500"
                    inputBox.Text = ""
                end
            end
        end
        
        confirmBtn.MouseButton1Click:Connect(function()
            applySpeed()
        end)
        
        inputBox.FocusLost:Connect(function(enterPressed)
            if enterPressed then
                applySpeed()
            end
        end)
        
        inputBox:CaptureFocus()
    end

    -- ======================== MENU DE VELOCIDADE DO FLY COM INPUT ========================
    
    function openFlySpeedMenu()
        local flySpeedGui = Instance.new("ScreenGui")
        flySpeedGui.Name = "FlySpeedGui"
        flySpeedGui.ResetOnSpawn = false
        flySpeedGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        flySpeedGui.Parent = playerGui
        
        local flySpeedFrame = Instance.new("Frame")
        flySpeedFrame.Name = "FlySpeedFrame"
        flySpeedFrame.Size = UDim2.new(0, 350, 0, 200)
        flySpeedFrame.Position = UDim2.new(0.5, -175, 0.5, -100)
        flySpeedFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        flySpeedFrame.BorderColor3 = Color3.fromRGB(100, 149, 237)
        flySpeedFrame.BorderSizePixel = 3
        flySpeedFrame.ZIndex = 999999
        flySpeedFrame.Parent = flySpeedGui
        
        local titleLabel = Instance.new("TextLabel")
        titleLabel.Name = "Title"
        titleLabel.Size = UDim2.new(1, 0, 0, 40)
        titleLabel.Position = UDim2.new(0, 0, 0, 0)
        titleLabel.BackgroundColor3 = Color3.fromRGB(100, 149, 237)
        titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        titleLabel.TextSize = 16
        titleLabel.Font = Enum.Font.GothamBold
        titleLabel.Text = lang.selectFlySpeed
        titleLabel.ZIndex = 999999
        titleLabel.Parent = flySpeedFrame
        
        local inputBox = Instance.new("TextBox")
        inputBox.Name = "FlySpeedInput"
        inputBox.Size = UDim2.new(0.8, 0, 0, 50)
        inputBox.Position = UDim2.new(0.1, 0, 0.25, 0)
        inputBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
        inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
        inputBox.TextSize = 18
        inputBox.Font = Enum.Font.GothamBold
        inputBox.PlaceholderText = "Digite: 10-10000"
        inputBox.PlaceholderColor3 = Color3.fromRGB(150, 150, 150)
        inputBox.BorderColor3 = Color3.fromRGB(100, 149, 237)
        inputBox.BorderSizePixel = 2
        inputBox.ZIndex = 999999
        inputBox.Parent = flySpeedFrame
        
        local confirmBtn = Instance.new("TextButton")
        confirmBtn.Name = "ConfirmBtn"
        confirmBtn.Size = UDim2.new(0.8, 0, 0, 40)
        confirmBtn.Position = UDim2.new(0.1, 0, 0.65, 0)
        confirmBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
        confirmBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
        confirmBtn.TextSize = 16
        confirmBtn.Font = Enum.Font.GothamBold
        confirmBtn.Text = "✅ Confirmar"
        confirmBtn.BorderColor3 = Color3.fromRGB(100, 149, 237)
        confirmBtn.BorderSizePixel = 2
        confirmBtn.ZIndex = 999999
        confirmBtn.Parent = flySpeedFrame
        
        local function applyFlySpeed()
            local inputValue = tonumber(inputBox.Text)
            if inputValue then
                if inputValue >= 10 and inputValue <= 10000 then
                    flySpeed = inputValue
                    startFly()
                    print("✅ Velocidade do Fly: " .. inputValue)
                    flySpeedGui:Destroy()
                else
                    inputBox.PlaceholderText = "Mín: 10, Máx: 10000"
                    inputBox.Text = ""
                end
            end
        end
        
        confirmBtn.MouseButton1Click:Connect(function()
            applyFlySpeed()
        end)
        
        inputBox.FocusLost:Connect(function(enterPressed)
            if enterPressed then
                applyFlySpeed()
            end
        end)
        
        inputBox:CaptureFocus()
    end

    -- ======================== KEYBOARD CONTROLS ========================
    
    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        
        if input.KeyCode == Enum.KeyCode.W then control.forward = 1 end
        if input.KeyCode == Enum.KeyCode.S then control.back = 1 end
        if input.KeyCode == Enum.KeyCode.A then control.left = 1 end
        if input.KeyCode == Enum.KeyCode.D then control.right = 1 end
        if input.KeyCode == Enum.KeyCode.Space then control.up = 1 end
        if input.KeyCode == Enum.KeyCode.LeftShift then control.down = 1 end
    end)
    
    UserInputService.InputEnded:Connect(function(input)
        if input.KeyCode == Enum.KeyCode.W then control.forward = 0 end
        if input.KeyCode == Enum.KeyCode.S then control.back = 0 end
        if input.KeyCode == Enum.KeyCode.A then control.left = 0 end
        if input.KeyCode == Enum.KeyCode.D then control.right = 0 end
        if input.KeyCode == Enum.KeyCode.Space then control.up = 0 end
        if input.KeyCode == Enum.KeyCode.LeftShift then control.down = 0 end
    end)

    -- ======================== ATUALIZAR VELOCIDADE DE CAMINHADA ========================
    
    function updateWalkSpeed()
        local character = player.Character
        if character then
            local humanoid = character:FindFirstChild("Humanoid")
            if humanoid then
                humanoid.WalkSpeed = walkSpeed
            end
        end
    end
    
    player.CharacterAdded:Connect(function(newCharacter)
        task.wait(0.3)
        if speedActive then
            local newHumanoid = newCharacter:FindFirstChild("Humanoid")
            if newHumanoid then
                newHumanoid.WalkSpeed = walkSpeed
            end
        end
        if flying then
            stopFly()
            task.wait(0.1)
            startFly()
        end
    end)

    -- ======================== FLY FUNCTIONS ========================
    
    function startFly()
        local char = player.Character
        if not char then return end
        
        local hrp = char:FindFirstChild("HumanoidRootPart")
        local humanoid = char:FindFirstChild("Humanoid")
        
        if not hrp or not humanoid then return end
        
        print("✈️ FLY INICIADO COM VELOCIDADE: " .. flySpeed)
        
        local oldBV = hrp:FindFirstChild("BodyVelocity")
        if oldBV then oldBV:Destroy() end
        local oldBG = hrp:FindFirstChild("BodyGyro")
        if oldBG then oldBG:Destroy() end
        
        bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.Velocity = Vector3.new(0, 0, 0)
        bodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        bodyVelocity.Parent = hrp
        
        bodyGyro = Instance.new("BodyGyro")
        bodyGyro.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
        bodyGyro.P = 10000
        bodyGyro.CFrame = hrp.CFrame
        bodyGyro.Parent = hrp
        
        humanoid.PlatformStand = false
        
        if flyConnection then
            flyConnection:Disconnect()
        end
        
        flyConnection = RunService.RenderStepped:Connect(function()
            if not flying or not char.Parent or not hrp.Parent then
                return
            end
            
            local cam = Camera
            local moveDir = Vector3.new(0, 0, 0)
            
            if control.forward == 1 then moveDir = moveDir + cam.CFrame.LookVector end
            if control.back == 1 then moveDir = moveDir - cam.CFrame.LookVector end
            if control.right == 1 then moveDir = moveDir + cam.CFrame.RightVector end
            if control.left == 1 then moveDir = moveDir - cam.CFrame.RightVector end
            if control.up == 1 then moveDir = moveDir + Vector3.new(0, 1, 0) end
            if control.down == 1 then moveDir = moveDir - Vector3.new(0, 1, 0) end
            
            if moveDir.Magnitude > 0 then
                moveDir = moveDir.Unit
            end
            
            bodyVelocity.Velocity = moveDir * flySpeed
            bodyGyro.CFrame = cam.CFrame
        end)
    end

    function stopFly()
        if flyConnection then
            flyConnection:Disconnect()
            flyConnection = nil
        end
        
        local char = player.Character
        if char then
            local hrp = char:FindFirstChild("HumanoidRootPart")
            if hrp then
                if bodyVelocity then
                    bodyVelocity:Destroy()
                    bodyVelocity = nil
                end
                if bodyGyro then
                    bodyGyro:Destroy()
                    bodyGyro = nil
                end
            end
        end
        print("✈️ FLY PARADO!")
    end

    -- ======================== FUNCIONALIDADES ========================

    -- Super Jump
    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        if input.KeyCode == Enum.KeyCode.Space and superJumpActive and not superJumpCooldown and not flying then
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
        if input.KeyCode == Enum.KeyCode.Space and infiniteJumpActive and not flying then
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

    function enableInvisibility()
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

    function disableInvisibility()
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

    function addESPToCharacter(character)
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

    function enableESP()
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

    function disableESP()
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
