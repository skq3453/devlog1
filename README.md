## Get Stuff
```lua
-->> Themes <<--
local Halloween = Color3.fromRGB(255, 60, 1) --october
local Christmas = Color3.fromRGB(250, 0, 0) --chrtismas
local July = Color3.fromRGB(0, 85, 255) --july
local Regular = Color3.fromRGB(49, 0, 148)

local lib = {}

function lib:CreateWindow(title)
	local UI = Instance.new("ScreenGui")
	local Main = Instance.new("Frame")
	local UICorner = Instance.new("UICorner")
	local Title = Instance.new("TextLabel")
	local Line = Instance.new("Frame")
	local Navigation = Instance.new("ScrollingFrame")
	local UIListLayout = Instance.new("UIListLayout")
	local UIPadding = Instance.new("UIPadding")
	local Line_2 = Instance.new("Frame")
	local Content = Instance.new("Frame")
	local ToggleUI = Instance.new("ImageButton")
	local UICorner_11 = Instance.new("UICorner")
	
	UI.Name = "UI"
	UI.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
	UI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	UI.ResetOnSpawn = false

	Main.Name = "Main"
	Main.Parent = UI
	Main.BackgroundColor3 = Color3.fromRGB(11, 11, 11)
	Main.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Main.BorderSizePixel = 0
	Main.Position = UDim2.new(0, 404, 0, 150)
	Main.Size = UDim2.new(0, 468, 0, 304)

	UICorner.Parent = Main

	Title.Name = "Title"
	Title.Parent = Main
	Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Title.BackgroundTransparency = 1.000
	Title.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Title.BorderSizePixel = 0
	Title.Position = UDim2.new(0.0170940179, 0, 0.0559210517, 0)
	Title.Size = UDim2.new(0, 140, 0, 42)
	Title.Font = Enum.Font.SourceSansBold
	Title.Text = title
	Title.TextColor3 = Color3.fromRGB(255, 255, 255)
	Title.TextSize = 28.000
	
	local currentMonth = os.date("*t").month

	if currentMonth == 12 then
		Title.Text = title .. " 🎁"  -- December: Gift emoji
	elseif currentMonth == 10 or 11 then
		Title.Text = title .. " 🎃"  -- October: Pumpkin emoji
	elseif currentMonth == 7 or 8 then
		Title.Text = title .. " 🎇"  -- July: Fireworks emoji
	else
		Title.Text = title  -- Default title for other months
	end

	Line.Name = "Line"
	Line.Parent = Main
	Line.BackgroundColor3 = Color3.fromRGB(51, 51, 51)
	Line.BackgroundTransparency = 0.500
	Line.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Line.BorderSizePixel = 0
	Line.Position = UDim2.new(0.0170940179, 0, 0.194078952, 0)
	Line.Size = UDim2.new(0, 132, 0, 1)

	Navigation.Name = "Navigation"
	Navigation.Parent = Main
	Navigation.Active = true
	Navigation.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Navigation.BackgroundTransparency = 1.000
	Navigation.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Navigation.BorderSizePixel = 0
	Navigation.Position = UDim2.new(0.0170940179, 0, 0.220394731, 0)
	Navigation.Size = UDim2.new(0, 140, 0, 227)
	Navigation.ScrollBarImageColor3 = Color3.fromRGB(0, 0, 0)
	Navigation.ScrollBarThickness = 0

	UIListLayout.Parent = Navigation
	UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.Padding = UDim.new(0, 4)

	UIPadding.Parent = Navigation
	UIPadding.PaddingTop = UDim.new(0, 2)
	
	Line_2.Name = "Line"
	Line_2.Parent = Main
	Line_2.BackgroundColor3 = Color3.fromRGB(51, 51, 51)
	Line_2.BackgroundTransparency = 0.500
	Line_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Line_2.BorderSizePixel = 0
	Line_2.Position = UDim2.new(0.316239327, 0, 0, 0)
	Line_2.Size = UDim2.new(0, 1, 0, 304)

	Content.Name = "Content"
	Content.Parent = Main
	Content.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Content.BackgroundTransparency = 1.000
	Content.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Content.BorderSizePixel = 0
	Content.Position = UDim2.new(0.318376064, 0, 0, 0)
	Content.Size = UDim2.new(0, 319, 0, 304)
	
	
	local function EDAEVXT_script() -- Main.dragWindow 
		local script = Instance.new('LocalScript', Main)

		local TweenService = game:GetService("TweenService")
		local UserInputService = game:GetService("UserInputService")

		local gui = script.Parent

		local dragging
		local dragInput
		local dragStart
		local startPos

		local tweenInfo = TweenInfo.new(0.16, Enum.EasingStyle.Linear, Enum.EasingDirection.Out)

		local function update(input)
			local delta = input.Position - dragStart
			local targetPos = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)

			local tween = TweenService:Create(gui, tweenInfo, {Position = targetPos})
			tween:Play()
		end

		gui.InputBegan:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				dragging = true
				dragStart = input.Position
				startPos = gui.Position

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

		UserInputService.InputChanged:Connect(function(input)
			if input == dragInput and dragging then
				update(input)
			end
		end)

	end
	coroutine.wrap(EDAEVXT_script)()
	
	ToggleUI.Name = "ToggleUI"
	ToggleUI.Parent = UI
	ToggleUI.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	ToggleUI.BorderColor3 = Color3.fromRGB(0, 0, 0)
	ToggleUI.BorderSizePixel = 0
	ToggleUI.Position = UDim2.new(0.351890743, 0, 0.280898869, 0)
	ToggleUI.Size = UDim2.new(0, 56, 0, 54)
	ToggleUI.AutoButtonColor = false
	ToggleUI.Image = "http://www.roblox.com/asset/?id=8249866376"

	UICorner_11.Parent = ToggleUI
	

	local function UNHXT_script() -- ToggleUI.dragButton 
		local script = Instance.new('LocalScript', ToggleUI)

		local TweenService = game:GetService("TweenService")
		local UserInputService = game:GetService("UserInputService")

		local gui = script.Parent

		local dragging
		local dragInput
		local dragStart
		local startPos

		local tweenInfo = TweenInfo.new(0.16, Enum.EasingStyle.Linear, Enum.EasingDirection.Out)

		local function update(input)
			local delta = input.Position - dragStart
			local targetPos = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)

			local tween = TweenService:Create(gui, tweenInfo, {Position = targetPos})
			tween:Play()
		end

		gui.InputBegan:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				dragging = true
				dragStart = input.Position
				startPos = gui.Position

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

		UserInputService.InputChanged:Connect(function(input)
			if input == dragInput and dragging then
				update(input)
			end
		end)

	end
	coroutine.wrap(UNHXT_script)()
	local function XVFLNV_script() -- UI.buttonToggle 
		local script = Instance.new('LocalScript', UI)

		local screenGui = script.Parent
		local button = screenGui:WaitForChild("ToggleUI")
		local main = screenGui:WaitForChild("Main")

		local function toggleVisibility()
			if main.Visible then
				main.Visible = false
			else
				main.Visible = true
			end
		end

		button.MouseButton1Click:Connect(toggleVisibility)
	end
	coroutine.wrap(XVFLNV_script)()
	
	local selectedTab = nil

	function lib:CreateTab(title)
		local Tab = Instance.new("TextButton")
		local UICorner_3 = Instance.new("UICorner")
		local Items = Instance.new("ScrollingFrame")
		local UIListLayout_2 = Instance.new("UIListLayout")
		local UIPadding_2 = Instance.new("UIPadding")

		Tab.Name = "Tab"
		Tab.Parent = Navigation
		Tab.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
		Tab.BackgroundTransparency = 1.000
		Tab.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Tab.BorderSizePixel = 0
		Tab.Position = UDim2.new(0.0571428575, 0, 0, 0)
		Tab.Size = UDim2.new(0, 124, 0, 37)
		Tab.AutoButtonColor = false
		Tab.Font = Enum.Font.SourceSans
		Tab.Text = title
		Tab.TextColor3 = Color3.fromRGB(255, 255, 255)
		Tab.TextSize = 18.000
		Tab.TextStrokeTransparency = 0.000

		UICorner_3.CornerRadius = UDim.new(0, 6)
		UICorner_3.Parent = Tab

		Items.Name = title
		Items.Parent = Content
		Items.Active = true
		Items.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Items.BackgroundTransparency = 1.000
		Items.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Items.BorderSizePixel = 0
		Items.Size = UDim2.new(0, 319, 0, 304)
		Items.ScrollBarImageColor3 = Color3.fromRGB(0, 0, 0)
		Items.ScrollBarThickness = 0
		Items.Visible = false

		UIListLayout_2.Parent = Items
		UIListLayout_2.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout_2.Padding = UDim.new(0, 4)

		UIPadding_2.Parent = Items
		UIPadding_2.PaddingTop = UDim.new(0, 6)

		if not selectedTab then
			selectedTab = Tab
			Tab.BackgroundTransparency = 0
			Tab.TextColor3 = Halloween
			Items.Visible = true
		end

		Tab.MouseButton1Click:Connect(function()
			if selectedTab ~= Tab then
				local prevItems = Content:FindFirstChild(selectedTab.Text)
				if prevItems then
					prevItems.Visible = false
				end

				selectedTab.BackgroundTransparency = 1
				selectedTab.TextColor3 = Color3.fromRGB(255, 255, 255)

				selectedTab = Tab
				Tab.BackgroundTransparency = 0
				Tab.TextColor3 = Halloween

				Items.Visible = true
			end
		end)

		return Tab, Items
	end
	
	function lib:CreateSection(title, TabParent)
		local Section = Instance.new("TextLabel")
		
		Section.Name = "Section"
		Section.Parent = TabParent
		Section.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Section.BackgroundTransparency = 1.000
		Section.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Section.BorderSizePixel = 0
		Section.Position = UDim2.new(0.0407523513, 0, 0, 0)
		Section.Size = UDim2.new(0, 301, 0, 32)
		Section.Font = Enum.Font.SourceSans
		Section.Text = title
		Section.TextColor3 = Color3.fromRGB(255, 255, 255)
		Section.TextSize = 18.000
		Section.TextTransparency = 0.600
		Section.TextXAlignment = Enum.TextXAlignment.Left
	end
	
	local TweenService = game:GetService("TweenService")

	function lib:CreateToggle(title, TabParent, callback)
		local Toggle = Instance.new("ImageButton")
		local UICorner_6 = Instance.new("UICorner")
		local Title_3 = Instance.new("TextLabel")
		local Checkbox_2 = Instance.new("Frame")
		local UICorner_7 = Instance.new("UICorner")

		Toggle.Name = "Toggle"
		Toggle.Parent = TabParent
		Toggle.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
		Toggle.BackgroundTransparency = 0.500
		Toggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Toggle.BorderSizePixel = 0
		Toggle.Position = UDim2.new(0.023510972, 0, 0.120805368, 0)
		Toggle.Size = UDim2.new(0, 304, 0, 40)
		Toggle.AutoButtonColor = false

		UICorner_6.CornerRadius = UDim.new(0, 4)
		UICorner_6.Parent = Toggle

		Title_3.Name = "Title"
		Title_3.Parent = Toggle
		Title_3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Title_3.BackgroundTransparency = 1.000
		Title_3.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Title_3.BorderSizePixel = 0
		Title_3.Position = UDim2.new(0.0308839902, 0, 0.140038297, 0)
		Title_3.Size = UDim2.new(0, 178, 0, 27)
		Title_3.Font = Enum.Font.SourceSans
		Title_3.Text = title
		Title_3.TextColor3 = Color3.fromRGB(255, 255, 255)
		Title_3.TextSize = 18.000
		Title_3.TextWrapped = true
		Title_3.TextXAlignment = Enum.TextXAlignment.Left

		Checkbox_2.Name = "Checkbox"
		Checkbox_2.Parent = Toggle
		Checkbox_2.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
		Checkbox_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Checkbox_2.BorderSizePixel = 0
		Checkbox_2.Position = UDim2.new(0.865131557, 0, 0.111363605, 0)
		Checkbox_2.Size = UDim2.new(0, 33, 0, 31)

		UICorner_7.CornerRadius = UDim.new(0, 4)
		UICorner_7.Parent = Checkbox_2

		local isToggled = false

		local function setCheckboxColor()
			local goalColor
			if isToggled then
				goalColor = Halloween
			else
				goalColor = Color3.fromRGB(21, 21, 21)
			end

			local tweenInfo = TweenInfo.new(0.1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out)
			local tween = TweenService:Create(Checkbox_2, tweenInfo, {BackgroundColor3 = goalColor})
			tween:Play()
		end

		local function onTogglePressed()
			isToggled = not isToggled
			setCheckboxColor()
			if callback then
				callback(isToggled)
			end
		end

		Toggle.MouseButton1Click:Connect(onTogglePressed)
		Toggle.TouchTap:Connect(onTogglePressed)

		setCheckboxColor()
	end
	
	function lib:CreateSlider(title, TabParent, min, max, callback)
		local Slider = Instance.new("ImageButton")
		local UICorner_8 = Instance.new("UICorner")
		local Title_4 = Instance.new("TextLabel")
		local SliderBack = Instance.new("Frame")
		local UICorner_9 = Instance.new("UICorner")
		local Draggable = Instance.new("Frame")
		local UICorner_10 = Instance.new("UICorner")
		local Value = Instance.new("TextLabel")
		local UIS = game:GetService("UserInputService")

		Slider.Name = "Slider"
		Slider.Parent = TabParent
		Slider.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
		Slider.BackgroundTransparency = 0.500
		Slider.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Slider.BorderSizePixel = 0
		Slider.Position = UDim2.new(0.023510972, 0, 0.120805368, 0)
		Slider.Size = UDim2.new(0, 304, 0, 40)
		Slider.AutoButtonColor = false

		UICorner_8.CornerRadius = UDim.new(0, 4)
		UICorner_8.Parent = Slider
		Title_4.Name = "Title"
		Title_4.Parent = Slider
		Title_4.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Title_4.BackgroundTransparency = 1.000
		Title_4.Position = UDim2.new(0.0308839902, 0, 0.140038297, 0)
		Title_4.Size = UDim2.new(0, 178, 0, 27)
		Title_4.Font = Enum.Font.SourceSans
		Title_4.Text = title
		Title_4.TextColor3 = Color3.fromRGB(255, 255, 255)
		Title_4.TextSize = 18.000
		Title_4.TextWrapped = true
		Title_4.TextXAlignment = Enum.TextXAlignment.Left

		SliderBack.Name = "SliderBack"
		SliderBack.Parent = Slider
		SliderBack.BackgroundColor3 = Color3.fromRGB(11, 11, 11)
		SliderBack.BorderColor3 = Color3.fromRGB(0, 0, 0)
		SliderBack.Position = UDim2.new(0.335526317, 0, 0.425000012, 0)
		SliderBack.Size = UDim2.new(0, 161, 0, 9)

		UICorner_9.CornerRadius = UDim.new(0, 4)
		UICorner_9.Parent = SliderBack

		Draggable.Name = "Draggable"
		Draggable.Parent = SliderBack
		Draggable.BackgroundColor3 = Halloween
		Draggable.Size = UDim2.new(0, 100, 0, 9)

		UICorner_10.CornerRadius = UDim.new(0, 4)
		UICorner_10.Parent = Draggable

		Value.Name = "Value"
		Value.Parent = Slider
		Value.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Value.BackgroundTransparency = 1.000
		Value.Position = UDim2.new(0.836805046, 0, 0.140038297, 0)
		Value.Size = UDim2.new(0, 41, 0, 27)
		Value.Font = Enum.Font.SourceSans
		Value.Text = string.format("%.1f", min)
		Value.TextColor3 = Color3.fromRGB(255, 255, 255)
		Value.TextSize = 18.000
		Value.TextWrapped = true
		Value.TextXAlignment = Enum.TextXAlignment.Right

		local currentValue = min
		local isDragging = false
		local touchID = nil

		local function UpdateSliderPosition()
			local percentage = math.clamp((currentValue - min) / (max - min), 0, 1)
			Value.Text = string.format("%.1f", currentValue)
			Draggable.Size = UDim2.new(percentage, 0, 1, 0)
			if callback then
				callback(currentValue)
			end
		end

		local function StartDragging(input)
			isDragging = true
			if input.UserInputType == Enum.UserInputType.Touch then
				touchID = input.UserInputIndex
			end
		end

		local function UpdateDragging(input)
			local inputPosition
			if input.UserInputType == Enum.UserInputType.MouseMovement then
				inputPosition = input.Position.X
			elseif input.UserInputType == Enum.UserInputType.Touch then
				inputPosition = input.Position.X
			end

			if isDragging then
				local sliderX = SliderBack.AbsolutePosition.X
				local sliderWidth = SliderBack.AbsoluteSize.X
				local newPercentage = math.clamp((inputPosition - sliderX) / sliderWidth, 0, 1)
				currentValue = min + (newPercentage * (max - min))
				currentValue = math.round(currentValue * 10) / 10
				UpdateSliderPosition()
			end
		end

		local function StopDragging(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				isDragging = false
				touchID = nil
			end
		end

		Slider.MouseButton1Down:Connect(StartDragging)
		UIS.InputChanged:Connect(UpdateDragging)
		UIS.InputEnded:Connect(StopDragging)

		UpdateSliderPosition()
	end
	
	return lib
end
```
## Create Window
```lua
lib:CreateWindow("Proxy")
```
## Create Tab
```lua
local tab1, tab1 = lib:CreateTab("Magnets")
```
## Create Section
```lua
lib:CreateSection("Magnet Settings", tab1)
```
## Create Toggle
```lua
lib:CreateToggle("Test Toggle", tab1, function(state)
	print(state)
end)
```
## Create Slider
```lua
lib:CreateSlider("Volume", tab1, 0, 100, function(value)
	print("Current Value: " .. value)
end)
```
