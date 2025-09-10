do
    local Console = game:GetService("CoreGui"):FindFirstChild("STX_Console")
    if Console then
        Console:Destroy()
    end
end

local Console = {}

local function pretty_date(date)
    local dateString = "{year}-{month}-{day} {hour}:{min}"
    local result = string.gsub(dateString, "{(%w+)}", date)
    return result
end

local now = os.time()

function Console:Window(consoledebugger)
    local Title = tostring(consoledebugger.Title)
    local GuiPosition = consoledebugger.Position
    local DragSpeed = consoledebugger.DragSpeed
    local Size = consoledebugger.Size or UDim2.new(0, 610, 0, 510)
    local CornerRadius = consoledebugger.CornerRadius or 10
    
    local STX_Console = Instance.new("ScreenGui")
    local ambientShadow = Instance.new("ImageLabel")
    local Window = Instance.new("Frame")
    local WindowUICorner = Instance.new("UICorner")
    local Outline_A = Instance.new("Frame")
    local ConsoleContainer = Instance.new("ScrollingFrame")
    local ConsoleContainerUICorner = Instance.new("UICorner")
    local ConsoleContainerUIListLayout = Instance.new("UIListLayout")
    local WindowTitle = Instance.new("TextLabel")
    local AutoScroll_Locked = Instance.new("Frame")
    local AutoScroll_LockedUICorner = Instance.new("UICorner")
    local AutoScroll_Locked_Inner = Instance.new("Frame")
    local AutoScroll_Locked_InnerUICorner = Instance.new("UICorner")
    local AutoScroll_Locked_Title = Instance.new("TextLabel")
    local AutoScroll_Locked_Title_2 = Instance.new("TextLabel")
    local ResizeHandle = Instance.new("ImageButton")
    local ResizeHandleUICorner = Instance.new("UICorner")
    
    STX_Console.Name = "STX_Console"
    STX_Console.Parent = game.CoreGui
    STX_Console.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    
    ambientShadow.Name = "ambientShadow"
    ambientShadow.Parent = STX_Console
    ambientShadow.AnchorPoint = Vector2.new(0.5, 0.5)
    ambientShadow.BackgroundTransparency = 1.000
    ambientShadow.BorderSizePixel = 0
    ambientShadow.Position = GuiPosition
    ambientShadow.Size = Size
    ambientShadow.Image = "rbxassetid://1316045217"
    ambientShadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
    ambientShadow.ImageTransparency = 0.400
    ambientShadow.ScaleType = Enum.ScaleType.Slice
    ambientShadow.SliceCenter = Rect.new(10, 10, 118, 118)

    local UserInputService = game:GetService("UserInputService")
    local runService = (game:GetService("RunService"));

    local gui = ambientShadow

    local dragging
    local dragInput
    local dragStart
    local startPos

    function Lerp(a, b, m)
        return a + (b - a) * m
    end;

    local lastMousePos
    local lastGoalPos
    local DRAG_SPEED = (DragSpeed); -- // The speed of the UI darg.
    function Update(dt)
        if not (startPos) then return end;
        if not (dragging) and (lastGoalPos) then
            gui.Position = UDim2.new(startPos.X.Scale, Lerp(gui.Position.X.Offset, lastGoalPos.X.Offset, dt * DRAG_SPEED), startPos.Y.Scale, Lerp(gui.Position.Y.Offset, lastGoalPos.Y.Offset, dt * DRAG_SPEED))
            return 
        end;

        local delta = (lastMousePos - UserInputService:GetMouseLocation())
        local xGoal = (startPos.X.Offset - delta.X);
        local yGoal = (startPos.Y.Offset - delta.Y);
        lastGoalPos = UDim2.new(startPos.X.Scale, xGoal, startPos.Y.Scale, yGoal)
        gui.Position = UDim2.new(startPos.X.Scale, Lerp(gui.Position.X.Offset, xGoal, dt * DRAG_SPEED), startPos.Y.Scale, Lerp(gui.Position.Y.Offset, yGoal, dt * DRAG_SPEED))
    end;

    gui.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = gui.Position
            lastMousePos = UserInputService:GetMouseLocation()

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    gui.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)

    runService.Heartbeat:Connect(Update)
    
    Window.Name = "Window"
    Window.Parent = ambientShadow
    Window.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    Window.BorderSizePixel = 0
    Window.Position = UDim2.new(0, 5, 0, 5)
    Window.Size = UDim2.new(0, ambientShadow.Size.X.Offset - 10, 0, ambientShadow.Size.Y.Offset - 10)
    Window.ZIndex = 2
    
    WindowUICorner.CornerRadius = UDim.new(0, CornerRadius)
    WindowUICorner.Name = "WindowUICorner"
    WindowUICorner.Parent = Window
    
    Outline_A.Name = "Outline_A"
    Outline_A.Parent = Window
    Outline_A.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    Outline_A.BorderSizePixel = 0
    Outline_A.Position = UDim2.new(0, 0, 0, 40)
    Outline_A.Size = UDim2.new(1, 0, 0, 2)
    Outline_A.ZIndex = 5
    
    ConsoleContainer.Name = "ConsoleContainer"
    ConsoleContainer.Parent = Window
    ConsoleContainer.Active = true
    ConsoleContainer.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    ConsoleContainer.BackgroundTransparency = 1.000
    ConsoleContainer.BorderSizePixel = 0
    ConsoleContainer.Position = UDim2.new(0, 10, 0, 50)
    ConsoleContainer.Size = UDim2.new(1, -20, 1, -60)
    ConsoleContainer.ZIndex = 3
    ConsoleContainer.BottomImage = ""
    ConsoleContainer.CanvasSize = UDim2.new(0, 0, 0, 0)
    ConsoleContainer.ScrollBarThickness = 0
    ConsoleContainer.TopImage = ""
    
    ConsoleContainerUICorner.CornerRadius = UDim.new(0, CornerRadius - 2)
    ConsoleContainerUICorner.Name = "ConsoleContainerUICorner"
    ConsoleContainerUICorner.Parent = ConsoleContainer
    
    ConsoleContainerUIListLayout.Name = "ConsoleContainerUIListLayout"
    ConsoleContainerUIListLayout.Parent = ConsoleContainer
    ConsoleContainerUIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
    ConsoleContainerUIListLayout.Padding = UDim.new(0, 10)
    
    WindowTitle.Name = "WindowTitle"
    WindowTitle.Parent = Window
    WindowTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    WindowTitle.BackgroundTransparency = 1.000
    WindowTitle.BorderColor3 = Color3.fromRGB(27, 42, 53)
    WindowTitle.BorderSizePixel = 0
    WindowTitle.Position = UDim2.new(0, 14, 0, 2)
    WindowTitle.Size = UDim2.new(0, 323, 0, 40)
    WindowTitle.ZIndex = 4
    WindowTitle.Font = Enum.Font.GothamSemibold
    WindowTitle.Text = Title
    WindowTitle.TextColor3 = Color3.fromRGB(220, 220, 220)
    WindowTitle.TextSize = 14.000
    WindowTitle.TextXAlignment = Enum.TextXAlignment.Left
    
    AutoScroll_Locked.Name = "AutoScroll_Locked"
    AutoScroll_Locked.Parent = Window
    AutoScroll_Locked.BackgroundColor3 = Color3.fromRGB(58, 58, 58)
    AutoScroll_Locked.Position = UDim2.new(1, -116, 0, 11)
    AutoScroll_Locked.Size = UDim2.new(0, 32, 0, 20)
    AutoScroll_Locked.ZIndex = 3
    
    AutoScroll_LockedUICorner.CornerRadius = UDim.new(0, 1000)
    AutoScroll_LockedUICorner.Name = "AutoScroll_LockedUICorner"
    AutoScroll_LockedUICorner.Parent = AutoScroll_Locked
    
    AutoScroll_Locked_Inner.Name = "AutoScroll_Locked_Inner"
    AutoScroll_Locked_Inner.Parent = AutoScroll_Locked
    AutoScroll_Locked_Inner.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    AutoScroll_Locked_Inner.BorderSizePixel = 0
    AutoScroll_Locked_Inner.Position = UDim2.new(0, 2, 0, 2)
    AutoScroll_Locked_Inner.Size = UDim2.new(0, 16, 0, 16)
    AutoScroll_Locked_Inner.ZIndex = 4
    
    AutoScroll_Locked_InnerUICorner.CornerRadius = UDim.new(0, 1000)
    AutoScroll_Locked_InnerUICorner.Name = "AutoScroll_Locked_InnerUICorner"
    AutoScroll_Locked_InnerUICorner.Parent = AutoScroll_Locked_Inner
    
    AutoScroll_Locked_Title.Name = "AutoScroll_Locked_Title"
    AutoScroll_Locked_Title.Parent = Window
    AutoScroll_Locked_Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    AutoScroll_Locked_Title.BackgroundTransparency = 1.000
    AutoScroll_Locked_Title.BorderColor3 = Color3.fromRGB(27, 42, 53)
    AutoScroll_Locked_Title.BorderSizePixel = 0
    AutoScroll_Locked_Title.Position = UDim2.new(1, -202, 0, 14)
    AutoScroll_Locked_Title.Size = UDim2.new(0, 80, 0, 14)
    AutoScroll_Locked_Title.ZIndex = 4
    AutoScroll_Locked_Title.Font = Enum.Font.GothamSemibold
    AutoScroll_Locked_Title.Text = "Autoscroll"
    AutoScroll_Locked_Title.TextColor3 = Color3.fromRGB(100, 100, 100)
    AutoScroll_Locked_Title.TextSize = 14.000
    AutoScroll_Locked_Title.TextXAlignment = Enum.TextXAlignment.Left
    
    AutoScroll_Locked_Title_2.Name = "AutoScroll_Locked_Title"
    AutoScroll_Locked_Title_2.Parent = Window
    AutoScroll_Locked_Title_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    AutoScroll_Locked_Title_2.BackgroundTransparency = 1.000
    AutoScroll_Locked_Title_2.BorderColor3 = Color3.fromRGB(27, 42, 53)
    AutoScroll_Locked_Title_2.BorderSizePixel = 0
    AutoScroll_Locked_Title_2.Position = UDim2.new(1, -80, 0, 14)
    AutoScroll_Locked_Title_2.Size = UDim2.new(0, 70, 0, 14)
    AutoScroll_Locked_Title_2.ZIndex = 4
    AutoScroll_Locked_Title_2.Font = Enum.Font.GothamSemibold
    AutoScroll_Locked_Title_2.Text = "[RightAlt]"
    AutoScroll_Locked_Title_2.TextColor3 = Color3.fromRGB(220, 220, 220)
    AutoScroll_Locked_Title_2.TextSize = 14.000
    AutoScroll_Locked_Title_2.TextXAlignment = Enum.TextXAlignment.Left

    -- Resize Handle
    ResizeHandle.Name = "ResizeHandle"
    ResizeHandle.Parent = Window
    ResizeHandle.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    ResizeHandle.BackgroundTransparency = 1.000
    ResizeHandle.Position = UDim2.new(1, -20, 1, -20)
    ResizeHandle.Size = UDim2.new(0, 20, 0, 20)
    ResizeHandle.ZIndex = 5
    ResizeHandle.Image = "rbxassetid://3926305904"
    ResizeHandle.ImageRectOffset = Vector2.new(284, 4)
    ResizeHandle.ImageRectSize = Vector2.new(24, 24)
    ResizeHandle.ImageColor3 = Color3.fromRGB(120, 120, 120)
    
    ResizeHandleUICorner.CornerRadius = UDim.new(0, 4)
    ResizeHandleUICorner.Name = "ResizeHandleUICorner"
    ResizeHandleUICorner.Parent = ResizeHandle

    -- Resize functionality
    local resizing = false
    local startSize
    local startMousePos

    ResizeHandle.MouseButton1Down:Connect(function()
        resizing = true
        startSize = ambientShadow.Size
        startMousePos = UserInputService:GetMouseLocation()
    end)

    UserInputService.InputChanged:Connect(function(input)
        if resizing and input.UserInputType == Enum.UserInputType.MouseMovement then
            local mouseDelta = UserInputService:GetMouseLocation() - startMousePos
            local newSize = UDim2.new(0, math.max(400, startSize.X.Offset + mouseDelta.X), 0, math.max(300, startSize.Y.Offset + mouseDelta.Y))
            
            ambientShadow.Size = newSize
            Window.Size = UDim2.new(0, newSize.X.Offset - 10, 0, newSize.Y.Offset - 10)
            
            -- Update positions of elements that need to stay at the right edge
            AutoScroll_Locked.Position = UDim2.new(1, -116, 0, 11)
            AutoScroll_Locked_Title.Position = UDim2.new(1, -202, 0, 14)
            AutoScroll_Locked_Title_2.Position = UDim2.new(1, -80, 0, 14)
        end
    end)

    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            resizing = false
        end
    end)

    local function ResizeContainer()
        ConsoleContainer.CanvasSize = UDim2.new(0, 0, 0, ConsoleContainerUIListLayout.AbsoluteContentSize.Y + ConsoleContainerUIListLayout.Padding.Offset)
    end
    ConsoleContainerUIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(ResizeContainer)

    local UserInputService = game:GetService("UserInputService")

    local function onInputBegan(input, gameProcessed)
        if input.UserInputType == Enum.UserInputType.Keyboard then
            if input.KeyCode == Enum.KeyCode.RightAlt then
                STX_Console.Enabled = not STX_Console.Enabled
            end
        end
    end

    UserInputService.InputBegan:Connect(onInputBegan)

    local ConsoleLog = {}

    function ConsoleLog:Prompt(promptdebugger)
        local PromptTitle = promptdebugger.Title
        local Content = promptdebugger.Content or ""
        local Type = (string.lower(tostring(promptdebugger.Type)));

        local now = os.time()
        local Time = tostring(pretty_date(os.date("*t", now)))
        local DefaultTitle = "["..tostring(Time).."]".." "..tostring(PromptTitle)
        local SuccessTitle = "["..tostring(Time).."]".." {Success} : "..tostring(PromptTitle)
        local FailTitle = "["..tostring(Time).."]".." {Error} : "..tostring(PromptTitle)
        local WarningTitle = "["..tostring(Time).."]".." {Warning} : "..tostring(PromptTitle)
        local NofiticationTitle = "["..tostring(Time).."]".." {Nofitication} : "..tostring(PromptTitle)

        local TextLabel = Instance.new("TextLabel")

        TextLabel.Parent = ConsoleContainer
        TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        TextLabel.BackgroundTransparency = 1.000
        TextLabel.BorderSizePixel = 0
        TextLabel.Size = UDim2.new(1, 0, 0, 12)
        TextLabel.ZIndex = 4
        TextLabel.Font = Enum.Font.Code
        TextLabel.Text = "Nil"
        TextLabel.TextColor3 = Color3.fromRGB(220, 220, 220)
        TextLabel.TextSize = 14.000
        TextLabel.TextXAlignment = Enum.TextXAlignment.Left
        TextLabel.TextYAlignment = Enum.TextYAlignment.Top
        TextLabel.TextWrapped = true
        TextLabel.AutomaticSize = Enum.AutomaticSize.Y

        -- Add content if provided
        if Content ~= "" then
            DefaultTitle = DefaultTitle .. "\n" .. Content
            SuccessTitle = SuccessTitle .. "\n" .. Content
            FailTitle = FailTitle .. "\n" .. Content
            WarningTitle = WarningTitle .. "\n" .. Content
            NofiticationTitle = NofiticationTitle .. "\n" .. Content
        end

        --[[
            Properties
        ]]

        if Type == ("default") then
            TextLabel.Text = tostring(DefaultTitle)
            TextLabel.TextColor3 = Color3.fromRGB(220, 220, 220)
        elseif Type == ("success") then
            TextLabel.Text = tostring(SuccessTitle)
            TextLabel.TextColor3 = Color3.fromRGB(83, 230, 50)
        elseif Type == ("fail") then
            TextLabel.Text = tostring(FailTitle)
            TextLabel.TextColor3 = Color3.fromRGB(255, 84, 84)
        elseif Type == ("warning") then
            TextLabel.Text = tostring(WarningTitle)
            TextLabel.TextColor3 = Color3.fromRGB(202, 156, 107)
        elseif Type == ("nofitication") then
            TextLabel.Text = tostring(NofiticationTitle)
            TextLabel.TextColor3 = Color3.fromRGB(121, 130, 255)
        end

        -- Auto-scroll to bottom
        task.wait()
        ConsoleContainer.CanvasPosition = Vector2.new(0, ConsoleContainer.AbsoluteCanvasSize.Y)
    end

    function ConsoleLog:Button(buttonConfig)
        local button = Instance.new("TextButton")
        button.Name = "Button"
        button.Parent = Window
        button.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
        button.BorderSizePixel = 0
        button.Position = UDim2.new(0, 10, 0, 10)
        button.Size = UDim2.new(0, 100, 0, 25)
        button.ZIndex = 5
        button.Font = Enum.Font.GothamSemibold
        button.Text = buttonConfig.Title or "Button"
        button.TextColor3 = Color3.fromRGB(220, 220, 220)
        button.TextSize = 12.000
        
        local buttonCorner = Instance.new("UICorner")
        buttonCorner.CornerRadius = UDim.new(0, 4)
        buttonCorner.Parent = button
        
        button.MouseButton1Click:Connect(function()
            if buttonConfig.Callback then
                buttonConfig.Callback()
            end
        end)
        
        return button
    end

    function ConsoleLog:Toggle(toggleConfig)
        local toggle = Instance.new("TextButton")
        toggle.Name = "Toggle"
        toggle.Parent = Window
        toggle.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
        toggle.BorderSizePixel = 0
        toggle.Position = UDim2.new(0, 120, 0, 10)
        toggle.Size = UDim2.new(0, 100, 0, 25)
        toggle.ZIndex = 5
        toggle.Font = Enum.Font.GothamSemibold
        toggle.Text = toggleConfig.Title or "Toggle"
        toggle.TextColor3 = Color3.fromRGB(220, 220, 220)
        toggle.TextSize = 12.000
        
        local toggleCorner = Instance.new("UICorner")
        toggleCorner.CornerRadius = UDim.new(0, 4)
        toggleCorner.Parent = toggle
        
        local isToggled = toggleConfig.Default or false
        updateToggleAppearance()
        
        function updateToggleAppearance()
            if isToggled then
                toggle.BackgroundColor3 = Color3.fromRGB(60, 120, 60)
            else
                toggle.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
            end
        end
        
        toggle.MouseButton1Click:Connect(function()
            isToggled = not isToggled
            updateToggleAppearance()
            if toggleConfig.Callback then
                toggleConfig.Callback(isToggled)
            end
        end)
        
        return toggle
    end

    return ConsoleLog
end

return Console
