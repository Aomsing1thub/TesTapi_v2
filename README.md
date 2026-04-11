local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")
local Workspace = game:GetService("Workspace")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

local GUI_NAME = "TestSimpleUI"
local BASE_WIDTH = 360
local BASE_MIN_HEIGHT = 120
local TOP_BAR_HEIGHT = 52
local CONTENT_MARGIN = 16
local MAX_VISIBLE_CONTENT_HEIGHT = 280
local SHADOW_OFFSET = 6
local SCREEN_MARGIN = 16
local DRAG_EDGE_SIZE = 10
local DROPDOWN_OPTION_HEIGHT = 30
local DROPDOWN_OPTION_GAP = 6

local oldGui = CoreGui:FindFirstChild(GUI_NAME) or PlayerGui:FindFirstChild(GUI_NAME)
if oldGui then
    oldGui:Destroy()
end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = GUI_NAME
screenGui.ResetOnSpawn = false
screenGui.IgnoreGuiInset = true
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = CoreGui

local shadow = Instance.new("Frame")
shadow.Name = "Shadow"
shadow.AnchorPoint = Vector2.new(0.5, 0.5)
shadow.Position = UDim2.new(0.5, SHADOW_OFFSET, 0.5, SHADOW_OFFSET)
shadow.Size = UDim2.new(0, BASE_WIDTH, 0, BASE_MIN_HEIGHT)
shadow.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
shadow.BackgroundTransparency = 0.55
shadow.BorderSizePixel = 0
shadow.ZIndex = 0
shadow.Parent = screenGui

local shadowCorner = Instance.new("UICorner")
shadowCorner.CornerRadius = UDim.new(0, 18)
shadowCorner.Parent = shadow

local shadowScale = Instance.new("UIScale")
shadowScale.Parent = shadow

local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
mainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
mainFrame.Size = UDim2.new(0, BASE_WIDTH, 0, BASE_MIN_HEIGHT)
mainFrame.BackgroundColor3 = Color3.fromRGB(24, 26, 32)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.ZIndex = 1
mainFrame.Parent = screenGui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 18)
mainCorner.Parent = mainFrame

local mainStroke = Instance.new("UIStroke")
mainStroke.Color = Color3.fromRGB(58, 66, 82)
mainStroke.Thickness = 1
mainStroke.Transparency = 0.15
mainStroke.Parent = mainFrame

local mainScale = Instance.new("UIScale")
mainScale.Parent = mainFrame

local title = Instance.new("TextLabel")
title.Name = "Title"
title.Size = UDim2.new(1, -80, 0, 24)
title.Position = UDim2.new(0, CONTENT_MARGIN, 0, 16)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBold
title.Text = "Controls"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextSize = 18
title.TextXAlignment = Enum.TextXAlignment.Left
title.ZIndex = 3
title.Parent = mainFrame

local controlsHint = Instance.new("TextLabel")
controlsHint.Name = "ControlsHint"
controlsHint.Size = UDim2.new(1, -120, 0, 18)
controlsHint.Position = UDim2.new(0, CONTENT_MARGIN, 0, 36)
controlsHint.BackgroundTransparency = 1
controlsHint.Font = Enum.Font.Gotham
controlsHint.Text = "Copy a block below to add more controls."
controlsHint.TextColor3 = Color3.fromRGB(176, 183, 196)
controlsHint.TextSize = 11
controlsHint.TextXAlignment = Enum.TextXAlignment.Left
controlsHint.ZIndex = 3
controlsHint.Parent = mainFrame

local closeButton = Instance.new("TextButton")
closeButton.Name = "CloseButton"
closeButton.Size = UDim2.new(0, 28, 0, 28)
closeButton.Position = UDim2.new(1, -40, 0, 12)
closeButton.BackgroundColor3 = Color3.fromRGB(58, 39, 43)
closeButton.BorderSizePixel = 0
closeButton.Font = Enum.Font.GothamBold
closeButton.Text = "X"
closeButton.TextColor3 = Color3.fromRGB(255, 214, 214)
closeButton.TextSize = 12
closeButton.ZIndex = 4
closeButton.Parent = mainFrame

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(1, 0)
closeCorner.Parent = closeButton

local closeStroke = Instance.new("UIStroke")
closeStroke.Color = Color3.fromRGB(116, 67, 75)
closeStroke.Thickness = 1
closeStroke.Parent = closeButton

local controlsList = Instance.new("ScrollingFrame")
controlsList.Name = "ControlsList"
controlsList.Size = UDim2.new(1, -(CONTENT_MARGIN * 2), 0, 0)
controlsList.Position = UDim2.new(0, CONTENT_MARGIN, 0, TOP_BAR_HEIGHT)
controlsList.BackgroundTransparency = 1
controlsList.BorderSizePixel = 0
controlsList.CanvasSize = UDim2.new(0, 0, 0, 0)
controlsList.ScrollBarThickness = 5
controlsList.ScrollBarImageColor3 = Color3.fromRGB(75, 84, 104)
controlsList.ScrollingDirection = Enum.ScrollingDirection.Y
controlsList.AutomaticCanvasSize = Enum.AutomaticSize.None
controlsList.ZIndex = 3
controlsList.Parent = mainFrame

local listLayout = Instance.new("UIListLayout")
listLayout.Padding = UDim.new(0, 10)
listLayout.FillDirection = Enum.FillDirection.Vertical
listLayout.SortOrder = Enum.SortOrder.LayoutOrder
listLayout.Parent = controlsList

local topDragRegion = Instance.new("Frame")
topDragRegion.Name = "TopDragRegion"
topDragRegion.Size = UDim2.new(1, -60, 0, 34)
topDragRegion.Position = UDim2.new(0, 12, 0, 10)
topDragRegion.BackgroundTransparency = 1
topDragRegion.ZIndex = 9
topDragRegion.Parent = mainFrame

local leftDragRegion = Instance.new("Frame")
leftDragRegion.Name = "LeftDragRegion"
leftDragRegion.Size = UDim2.new(0, DRAG_EDGE_SIZE, 1, -24)
leftDragRegion.Position = UDim2.new(0, 0, 0, 12)
leftDragRegion.BackgroundTransparency = 1
leftDragRegion.ZIndex = 9
leftDragRegion.Parent = mainFrame

local rightDragRegion = Instance.new("Frame")
rightDragRegion.Name = "RightDragRegion"
rightDragRegion.Size = UDim2.new(0, DRAG_EDGE_SIZE, 1, -24)
rightDragRegion.Position = UDim2.new(1, -DRAG_EDGE_SIZE, 0, 12)
rightDragRegion.BackgroundTransparency = 1
rightDragRegion.ZIndex = 9
rightDragRegion.Parent = mainFrame

local bottomDragRegion = Instance.new("Frame")
bottomDragRegion.Name = "BottomDragRegion"
bottomDragRegion.Size = UDim2.new(1, -24, 0, DRAG_EDGE_SIZE)
bottomDragRegion.Position = UDim2.new(0, 12, 1, -DRAG_EDGE_SIZE)
bottomDragRegion.BackgroundTransparency = 1
bottomDragRegion.ZIndex = 9
bottomDragRegion.Parent = mainFrame

local reopenButton = Instance.new("TextButton")
reopenButton.Name = "ReopenButton"
reopenButton.AnchorPoint = Vector2.new(0, 1)
reopenButton.Size = UDim2.new(0, 42, 0, 42)
reopenButton.Position = UDim2.new(0, SCREEN_MARGIN, 1, -SCREEN_MARGIN)
reopenButton.BackgroundColor3 = Color3.fromRGB(78, 118, 214)
reopenButton.BorderSizePixel = 0
reopenButton.Font = Enum.Font.GothamBold
reopenButton.Text = "UI"
reopenButton.TextColor3 = Color3.fromRGB(255, 255, 255)
reopenButton.TextSize = 12
reopenButton.Visible = false
reopenButton.ZIndex = 6
reopenButton.Parent = screenGui

local reopenCorner = Instance.new("UICorner")
reopenCorner.CornerRadius = UDim.new(1, 0)
reopenCorner.Parent = reopenButton

local reopenStroke = Instance.new("UIStroke")
reopenStroke.Color = Color3.fromRGB(132, 170, 255)
reopenStroke.Thickness = 1
reopenStroke.Parent = reopenButton

local dragging = false
local dragInput
local dragStart
local frameStart
local currentHeight = BASE_MIN_HEIGHT
local viewportConnection

local function getViewportSize()
    local camera = Workspace.CurrentCamera
    if camera then
        return camera.ViewportSize
    end

    return Vector2.new(1366, 768)
end

local function clampWindowPosition(position)
    local viewport = getViewportSize()
    local scaledWidth = BASE_WIDTH * mainScale.Scale
    local scaledHeight = currentHeight * mainScale.Scale
    local horizontalLimit = math.max(0, ((viewport.X - scaledWidth) / 2) - SCREEN_MARGIN)
    local verticalLimit = math.max(0, ((viewport.Y - scaledHeight) / 2) - SCREEN_MARGIN)

    return UDim2.new(
        0.5,
        math.clamp(position.X.Offset, -horizontalLimit, horizontalLimit),
        0.5,
        math.clamp(position.Y.Offset, -verticalLimit, verticalLimit)
    )
end

local function syncShadow()
    shadow.Size = mainFrame.Size
    shadow.Position = UDim2.new(
        mainFrame.Position.X.Scale,
        mainFrame.Position.X.Offset + SHADOW_OFFSET,
        mainFrame.Position.Y.Scale,
        mainFrame.Position.Y.Offset + SHADOW_OFFSET
    )
end

local function updateResponsiveScale()
    local viewport = getViewportSize()
    local widthScale = (viewport.X - (SCREEN_MARGIN * 2)) / BASE_WIDTH
    local heightScale = (viewport.Y - (SCREEN_MARGIN * 2)) / currentHeight
    local targetScale = math.clamp(math.min(widthScale, heightScale, 1), 0.72, 1)

    mainScale.Scale = targetScale
    shadowScale.Scale = targetScale
    mainFrame.Position = clampWindowPosition(mainFrame.Position)
    syncShadow()
end

local function setWindowVisible(isVisible)
    mainFrame.Visible = isVisible
    shadow.Visible = isVisible
    reopenButton.Visible = not isVisible
end

local function updateWindowHeight()
    local contentHeight = listLayout.AbsoluteContentSize.Y
    local visibleContentHeight = math.min(contentHeight, MAX_VISIBLE_CONTENT_HEIGHT)

    controlsList.Size = UDim2.new(1, -(CONTENT_MARGIN * 2), 0, visibleContentHeight)
    controlsList.CanvasSize = UDim2.new(0, 0, 0, math.max(contentHeight, visibleContentHeight))
    currentHeight = math.max(BASE_MIN_HEIGHT, TOP_BAR_HEIGHT + visibleContentHeight + CONTENT_MARGIN)
    mainFrame.Size = UDim2.new(0, BASE_WIDTH, 0, currentHeight)
    updateResponsiveScale()
end

local function updateDrag(input)
    local delta = input.Position - dragStart
    local newPosition = UDim2.new(0.5, frameStart.X.Offset + delta.X, 0.5, frameStart.Y.Offset + delta.Y)
    mainFrame.Position = clampWindowPosition(newPosition)
    syncShadow()
end

local function bindDragSource(source)
    source.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragInput = input
            dragStart = input.Position
            frameStart = mainFrame.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                    dragInput = nil
                end
            end)
        end
    end)

    source.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)
end

local function createCardBase(cardClass, cardName, titleText, descriptionText, cardHeight, layoutOrder)
    local card = Instance.new(cardClass)
    card.Name = cardName
    card.Size = UDim2.new(1, 0, 0, cardHeight)
    card.BackgroundColor3 = Color3.fromRGB(31, 34, 42)
    card.BorderSizePixel = 0
    card.LayoutOrder = layoutOrder
    card.ZIndex = 3
    card.Parent = controlsList

    if card:IsA("TextButton") then
        card.Text = ""
        card.AutoButtonColor = false
    end

    local cardCorner = Instance.new("UICorner")
    cardCorner.CornerRadius = UDim.new(0, 12)
    cardCorner.Parent = card

    local cardStroke = Instance.new("UIStroke")
    cardStroke.Color = Color3.fromRGB(56, 64, 79)
    cardStroke.Thickness = 1
    cardStroke.Transparency = 0.2
    cardStroke.Parent = card

    local cardTitle = Instance.new("TextLabel")
    cardTitle.Name = "Title"
    cardTitle.Size = UDim2.new(1, -28, 0, 18)
    cardTitle.Position = UDim2.new(0, 14, 0, 8)
    cardTitle.BackgroundTransparency = 1
    cardTitle.Font = Enum.Font.GothamBold
    cardTitle.Text = titleText
    cardTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
    cardTitle.TextSize = 13
    cardTitle.TextXAlignment = Enum.TextXAlignment.Left
    cardTitle.ZIndex = 4
    cardTitle.Parent = card

    if descriptionText and descriptionText ~= "" then
        local cardDescription = Instance.new("TextLabel")
        cardDescription.Name = "Description"
        cardDescription.Size = UDim2.new(1, -28, 0, 16)
        cardDescription.Position = UDim2.new(0, 14, 0, 24)
        cardDescription.BackgroundTransparency = 1
        cardDescription.Font = Enum.Font.Gotham
        cardDescription.Text = descriptionText
        cardDescription.TextColor3 = Color3.fromRGB(176, 183, 196)
        cardDescription.TextSize = 11
        cardDescription.TextXAlignment = Enum.TextXAlignment.Left
        cardDescription.ZIndex = 4
        cardDescription.Parent = card
    end

    return card
end

local function getDropdownListHeight(optionCount)
    if optionCount == 0 then
        return 0
    end

    return (optionCount * DROPDOWN_OPTION_HEIGHT) + ((optionCount - 1) * DROPDOWN_OPTION_GAP)
end

local Section = {
    nextLayoutOrder = 0,
}

function Section:_nextOrder()
    self.nextLayoutOrder = self.nextLayoutOrder + 1
    return self.nextLayoutOrder
end

function Section:NewButton(name, callback)
    local card = createCardBase(
        "TextButton",
        (name:gsub("%s+", "") .. "ButtonCard"),
        name,
        "Press anywhere on this card.",
        48,
        self:_nextOrder()
    )

    card.MouseButton1Click:Connect(function()
        if callback then
            callback()
        end
    end)

    return card
end

function Section:NewToggle(name, defaultValue, callback)
    local card = createCardBase(
        "TextButton",
        (name:gsub("%s+", "") .. "ToggleCard"),
        name,
        "Tap the card or switch to toggle.",
        48,
        self:_nextOrder()
    )

    local toggleButton = Instance.new("TextButton")
    toggleButton.Name = "ToggleButton"
    toggleButton.Size = UDim2.new(0, 52, 0, 26)
    toggleButton.Position = UDim2.new(1, -66, 0.5, -13)
    toggleButton.BackgroundColor3 = Color3.fromRGB(52, 57, 70)
    toggleButton.BorderSizePixel = 0
    toggleButton.Text = ""
    toggleButton.AutoButtonColor = false
    toggleButton.ZIndex = 5
    toggleButton.Parent = card

    local toggleCorner = Instance.new("UICorner")
    toggleCorner.CornerRadius = UDim.new(1, 0)
    toggleCorner.Parent = toggleButton

    local toggleKnob = Instance.new("Frame")
    toggleKnob.Name = "ToggleKnob"
    toggleKnob.Size = UDim2.new(0, 20, 0, 20)
    toggleKnob.Position = UDim2.new(0, 3, 0.5, -10)
    toggleKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    toggleKnob.BorderSizePixel = 0
    toggleKnob.ZIndex = 6
    toggleKnob.Parent = toggleButton

    local toggleKnobCorner = Instance.new("UICorner")
    toggleKnobCorner.CornerRadius = UDim.new(1, 0)
    toggleKnobCorner.Parent = toggleKnob

    local toggleState = defaultValue == true

    local function applyToggleState(newState)
        toggleState = newState
        toggleButton.BackgroundColor3 = toggleState and Color3.fromRGB(91, 140, 255) or Color3.fromRGB(52, 57, 70)
        toggleKnob.Position = toggleState and UDim2.new(1, -23, 0.5, -10) or UDim2.new(0, 3, 0.5, -10)
    end

    local function triggerToggle()
        applyToggleState(not toggleState)
        if callback then
            callback(toggleState)
        end
    end

    applyToggleState(toggleState)

    card.MouseButton1Click:Connect(triggerToggle)
    toggleButton.MouseButton1Click:Connect(triggerToggle)

    return card
end

function Section:NewDropdown(name, options, callback)
    local dropdownOpen = false
    local selectedOption = options[1] or "None"

    local card = createCardBase(
        "Frame",
        (name:gsub("%s+", "") .. "DropdownCard"),
        name,
        "Edit options directly inside this block.",
        84,
        self:_nextOrder()
    )
    card.ClipsDescendants = true

    local dropdownButton = Instance.new("TextButton")
    dropdownButton.Name = "DropdownButton"
    dropdownButton.Size = UDim2.new(1, -28, 0, 30)
    dropdownButton.Position = UDim2.new(0, 14, 0, 46)
    dropdownButton.BackgroundColor3 = Color3.fromRGB(39, 43, 54)
    dropdownButton.BorderSizePixel = 0
    dropdownButton.Font = Enum.Font.Gotham
    dropdownButton.Text = ""
    dropdownButton.AutoButtonColor = false
    dropdownButton.ZIndex = 4
    dropdownButton.Parent = card

    local dropdownCorner = Instance.new("UICorner")
    dropdownCorner.CornerRadius = UDim.new(0, 10)
    dropdownCorner.Parent = dropdownButton

    local dropdownText = Instance.new("TextLabel")
    dropdownText.Name = "DropdownText"
    dropdownText.Size = UDim2.new(1, -40, 1, 0)
    dropdownText.Position = UDim2.new(0, 12, 0, 0)
    dropdownText.BackgroundTransparency = 1
    dropdownText.Font = Enum.Font.Gotham
    dropdownText.TextColor3 = Color3.fromRGB(235, 239, 245)
    dropdownText.TextSize = 12
    dropdownText.TextXAlignment = Enum.TextXAlignment.Left
    dropdownText.ZIndex = 5
    dropdownText.Parent = dropdownButton

    local dropdownArrow = Instance.new("TextLabel")
    dropdownArrow.Name = "DropdownArrow"
    dropdownArrow.Size = UDim2.new(0, 22, 1, 0)
    dropdownArrow.Position = UDim2.new(1, -26, 0, 0)
    dropdownArrow.BackgroundTransparency = 1
    dropdownArrow.Font = Enum.Font.GothamBold
    dropdownArrow.TextColor3 = Color3.fromRGB(161, 195, 255)
    dropdownArrow.TextSize = 14
    dropdownArrow.ZIndex = 5
    dropdownArrow.Parent = dropdownButton

    local dropdownList = Instance.new("Frame")
    dropdownList.Name = "DropdownList"
    dropdownList.Size = UDim2.new(1, -28, 0, 0)
    dropdownList.Position = UDim2.new(0, 14, 0, 82)
    dropdownList.BackgroundTransparency = 1
    dropdownList.BorderSizePixel = 0
    dropdownList.Visible = false
    dropdownList.ZIndex = 4
    dropdownList.Parent = card

    local function updateDropdownText()
        dropdownText.Text = "Selected: " .. selectedOption
        dropdownArrow.Text = dropdownOpen and "^" or "v"
    end

    local function refreshDropdownCard()
        local listHeight = dropdownOpen and getDropdownListHeight(#options) or 0
        card.Size = UDim2.new(1, 0, 0, 84 + listHeight)
        dropdownList.Size = UDim2.new(1, -28, 0, listHeight)
        dropdownList.Visible = dropdownOpen
        updateWindowHeight()
    end

    local function rebuildDropdownOptions()
        dropdownList:ClearAllChildren()

        for index, optionName in ipairs(options) do
            local optionButton = Instance.new("TextButton")
            optionButton.Name = "Option" .. index
            optionButton.Size = UDim2.new(1, 0, 0, DROPDOWN_OPTION_HEIGHT)
            optionButton.Position = UDim2.new(0, 0, 0, (index - 1) * (DROPDOWN_OPTION_HEIGHT + DROPDOWN_OPTION_GAP))
            optionButton.BackgroundColor3 = Color3.fromRGB(39, 43, 54)
            optionButton.BorderSizePixel = 0
            optionButton.Font = Enum.Font.Gotham
            optionButton.Text = optionName
            optionButton.TextColor3 = Color3.fromRGB(235, 239, 245)
            optionButton.TextSize = 12
            optionButton.AutoButtonColor = false
            optionButton.ZIndex = 5
            optionButton.Parent = dropdownList

            local optionCorner = Instance.new("UICorner")
            optionCorner.CornerRadius = UDim.new(0, 10)
            optionCorner.Parent = optionButton

            optionButton.MouseButton1Click:Connect(function()
                selectedOption = optionName
                dropdownOpen = false
                updateDropdownText()
                refreshDropdownCard()
                if callback then
                    callback(selectedOption)
                end
            end)
        end

        refreshDropdownCard()
    end

    rebuildDropdownOptions()
    updateDropdownText()

    dropdownButton.MouseButton1Click:Connect(function()
        dropdownOpen = not dropdownOpen
        updateDropdownText()
        refreshDropdownCard()
    end)

    return card
end

function Section:NewMultiDropdown(name, options, callback)
    local dropdownOpen = false
    local selectedLookup = {}
    local selectedOptions = {}

    local card = createCardBase(
        "Frame",
        (name:gsub("%s+", "") .. "MultiDropdownCard"),
        name,
        "Select multiple options from this list.",
        84,
        self:_nextOrder()
    )
    card.ClipsDescendants = true

    local dropdownButton = Instance.new("TextButton")
    dropdownButton.Name = "MultiDropdownButton"
    dropdownButton.Size = UDim2.new(1, -28, 0, 30)
    dropdownButton.Position = UDim2.new(0, 14, 0, 46)
    dropdownButton.BackgroundColor3 = Color3.fromRGB(39, 43, 54)
    dropdownButton.BorderSizePixel = 0
    dropdownButton.Font = Enum.Font.Gotham
    dropdownButton.Text = ""
    dropdownButton.AutoButtonColor = false
    dropdownButton.ZIndex = 4
    dropdownButton.Parent = card

    local dropdownCorner = Instance.new("UICorner")
    dropdownCorner.CornerRadius = UDim.new(0, 10)
    dropdownCorner.Parent = dropdownButton

    local dropdownText = Instance.new("TextLabel")
    dropdownText.Name = "MultiDropdownText"
    dropdownText.Size = UDim2.new(1, -40, 1, 0)
    dropdownText.Position = UDim2.new(0, 12, 0, 0)
    dropdownText.BackgroundTransparency = 1
    dropdownText.Font = Enum.Font.Gotham
    dropdownText.TextColor3 = Color3.fromRGB(235, 239, 245)
    dropdownText.TextSize = 12
    dropdownText.TextXAlignment = Enum.TextXAlignment.Left
    dropdownText.ZIndex = 5
    dropdownText.Parent = dropdownButton

    local dropdownArrow = Instance.new("TextLabel")
    dropdownArrow.Name = "MultiDropdownArrow"
    dropdownArrow.Size = UDim2.new(0, 22, 1, 0)
    dropdownArrow.Position = UDim2.new(1, -26, 0, 0)
    dropdownArrow.BackgroundTransparency = 1
    dropdownArrow.Font = Enum.Font.GothamBold
    dropdownArrow.TextColor3 = Color3.fromRGB(161, 195, 255)
    dropdownArrow.TextSize = 14
    dropdownArrow.ZIndex = 5
    dropdownArrow.Parent = dropdownButton

    local dropdownList = Instance.new("Frame")
    dropdownList.Name = "MultiDropdownList"
    dropdownList.Size = UDim2.new(1, -28, 0, 0)
    dropdownList.Position = UDim2.new(0, 14, 0, 82)
    dropdownList.BackgroundTransparency = 1
    dropdownList.BorderSizePixel = 0
    dropdownList.Visible = false
    dropdownList.ZIndex = 4
    dropdownList.Parent = card

    local function cloneSelectedOptions()
        local result = {}
        for index, optionName in ipairs(selectedOptions) do
            result[index] = optionName
        end
        return result
    end

    local function rebuildSelectedOptions()
        table.clear(selectedOptions)
        for _, optionName in ipairs(options) do
            if selectedLookup[optionName] then
                table.insert(selectedOptions, optionName)
            end
        end
    end

    local function updateDropdownText()
        if #selectedOptions == 0 then
            dropdownText.Text = "Selected: None"
        elseif #selectedOptions == 1 then
            dropdownText.Text = "Selected: " .. selectedOptions[1]
        elseif #selectedOptions == 2 then
            dropdownText.Text = "Selected: " .. selectedOptions[1] .. ", " .. selectedOptions[2]
        else
            dropdownText.Text = "Selected: " .. #selectedOptions .. " items"
        end

        dropdownArrow.Text = dropdownOpen and "^" or "v"
    end

    local function refreshDropdownCard()
        local listHeight = dropdownOpen and getDropdownListHeight(#options) or 0
        card.Size = UDim2.new(1, 0, 0, 84 + listHeight)
        dropdownList.Size = UDim2.new(1, -28, 0, listHeight)
        dropdownList.Visible = dropdownOpen
        updateWindowHeight()
    end

    local function rebuildDropdownOptions()
        dropdownList:ClearAllChildren()

        for index, optionName in ipairs(options) do
            local optionButton = Instance.new("TextButton")
            optionButton.Name = "Option" .. index
            optionButton.Size = UDim2.new(1, 0, 0, DROPDOWN_OPTION_HEIGHT)
            optionButton.Position = UDim2.new(0, 0, 0, (index - 1) * (DROPDOWN_OPTION_HEIGHT + DROPDOWN_OPTION_GAP))
            optionButton.BackgroundColor3 = selectedLookup[optionName] and Color3.fromRGB(67, 98, 168) or Color3.fromRGB(39, 43, 54)
            optionButton.BorderSizePixel = 0
            optionButton.Font = Enum.Font.Gotham
            optionButton.Text = optionName
            optionButton.TextColor3 = Color3.fromRGB(235, 239, 245)
            optionButton.TextSize = 12
            optionButton.AutoButtonColor = false
            optionButton.ZIndex = 5
            optionButton.Parent = dropdownList

            local optionCorner = Instance.new("UICorner")
            optionCorner.CornerRadius = UDim.new(0, 10)
            optionCorner.Parent = optionButton

            optionButton.MouseButton1Click:Connect(function()
                selectedLookup[optionName] = not selectedLookup[optionName] or nil
                rebuildSelectedOptions()
                updateDropdownText()
                rebuildDropdownOptions()
                if callback then
                    callback(cloneSelectedOptions())
                end
            end)
        end

        refreshDropdownCard()
    end

    rebuildSelectedOptions()
    rebuildDropdownOptions()
    updateDropdownText()

    dropdownButton.MouseButton1Click:Connect(function()
        dropdownOpen = not dropdownOpen
        updateDropdownText()
        refreshDropdownCard()
    end)

    return card
end

dataname = {}
Mydata = {}

for i,v in pairs (game:GetService("Players").LocalPlayer.PlayerGui.Tranformar.Characters:GetChildren()) do
	if v:IsA("ImageLabel") then
		-- print(v)
		table.insert(dataname,v.Name)
		-- game:GetService("ReplicatedStorage"):WaitForChild("SkillEvent"):FireServer(v.Name)
	end
end

for key, v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Tranformar.TrocarPersonagem.ScrollingFrame:GetChildren()) do
    if v:IsA("ImageButton") then
        if v.Visible then
            table.insert(Mydata,v.Name)
        end
    end
end

Section:NewDropdown("Characters", dataname, function(currentOption)
    game:GetService("ReplicatedStorage"):WaitForChild("MorphRequest"):FireServer(currentOption)
end)

Section:NewDropdown("Change Skill", Mydata, function(currentOption)
    firesignal(game:GetService("Players").LocalPlayer.PlayerGui.Tranformar.Characters[currentOption].Transform.MouseButton1Click)
end)

-- Section:NewButton("Button", function()
    
-- end)

Section:NewToggle("Toggle", false, function(state)
    a1 = state
    if not a1 then
        if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
            game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
        end 
    end
end)

Section:NewMultiDropdown("Characters Multi", Mydata, function(selectedOptions)
    game:GetService("Players").LocalPlayer.PlayerGui.Botoes.Direita.Visible = false
    if #selectedOptions == 1 then
        firesignal(game:GetService("Players").LocalPlayer.PlayerGui.Tranformar.Characters[selectedOptions[1]].Transform.MouseButton1Click)
    elseif #selectedOptions == 2 then
        target = game:GetService("Players").LocalPlayer.PlayerGui.Botoes.Poderes["TrolarBotão"]

        if target then
            cloned = target:Clone()
            cloned.Parent = target.Parent
            cloned.Name = "2_1"
            cloned.Position = target.Position - UDim2.new(0.731, 0, 0, 0)
            cloned.TextLabel.Name = selectedOptions[2]
        end

        if game:GetService("Players").LocalPlayer.PlayerGui.Botoes.Poderes:FindFirstChild("TrolarBotao2") then
            target = game:GetService("Players").LocalPlayer.PlayerGui.Botoes.Poderes["TrolarBotao2"]

            if target then
                cloned = target:Clone()
                cloned.Parent = target.Parent
                cloned.Name = "2_2"
                cloned.Position = target.Position - UDim2.new(0.731, 0, 0, 0)
                cloned.TextLabel.Name = selectedOptions[2].."2"
            end
        end
        firesignal(game:GetService("Players").LocalPlayer.PlayerGui.Tranformar.Characters[selectedOptions[2]].Transform.MouseButton1Click)
    end
end)

task.spawn(function()
while wait() do
if a1 then
pcall(function()
    if game.Players.LocalPlayer.Character.Humanoid.FloorMaterial ~= Enum.Material.Air and game.Players.LocalPlayer.Character.HumanoidRootPart.Position.Y > 30 and not stop then
        Save = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        wait(.5)
        if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
            game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ"):Destroy()
        end 
    end
end)
end
end
end)

task.spawn(function()
while task.wait() do
if a1 then
pcall(function()
    if game.Players.LocalPlayer.Character.HumanoidRootPart.Position.Y <= 28 then
        stop = true
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Save
        if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
            local Noclip = Instance.new("BodyVelocity")
            Noclip.Name = "GGEZ"
            Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
            Noclip.MaxForce = Vector3.new(100000,100000,100000)
            Noclip.Velocity = Vector3.new(0,0,0)
        end
        stop = false
    end
end)
end
end
end)

-- Middle -3.509385347366333, 27.93985939025879, 24.57699966430664
task.spawn(function()
while wait() do
if a1 then
pcall(function()
    if workspace.CurrentArena:FindFirstChild("Power Arena") then
        workspace.CurrentArena["Power Arena"].Arena.Piao.Cone:Destroy()
    end
    if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BallSocketConstraint") then
        if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("GGEZ") then
            local Noclip = Instance.new("BodyVelocity")
            Noclip.Name = "GGEZ"
            Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
            Noclip.MaxForce = Vector3.new(100000,100000,100000)
            Noclip.Velocity = Vector3.new(0,0,0)
        end
    end
end)
end
end
end)

local function connectViewportListener()
    if viewportConnection then
        viewportConnection:Disconnect()
        viewportConnection = nil
    end

    local camera = Workspace.CurrentCamera
    if camera then
        viewportConnection = camera:GetPropertyChangedSignal("ViewportSize"):Connect(updateResponsiveScale)
    end

    updateResponsiveScale()
end

-- Startup
Workspace:GetPropertyChangedSignal("CurrentCamera"):Connect(connectViewportListener)
updateWindowHeight()
connectViewportListener()

-- Event Connections
bindDragSource(topDragRegion)
bindDragSource(leftDragRegion)
bindDragSource(rightDragRegion)
bindDragSource(bottomDragRegion)

UserInputService.InputChanged:Connect(function(input)
    if dragging and input == dragInput then
        updateDrag(input)
    end
end)

listLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(updateWindowHeight)

closeButton.MouseButton1Click:Connect(function()
    setWindowVisible(false)
end)

reopenButton.MouseButton1Click:Connect(function()
    setWindowVisible(true)
    updateResponsiveScale()
end)
