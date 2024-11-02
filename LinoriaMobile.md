# Linoria Lib -But On Mobile-

made by the one and only [**jamkles**] skid as much as you need

### Library loadstring

```lua
     local repo = 'https://raw.githubusercontent.com/LionTheGreatRealFrFr/MobileLinoriaLib/main/'
```

### Theme and Save Manager

```lua
local Library = loadstring(game:HttpGet(repo .. 'Library.lua'))()
local ThemeManager = loadstring(game:HttpGet(repo .. 'addons/ThemeManager.lua'))()
local SaveManager = loadstring(game:HttpGet(repo .. 'addons/SaveManager.lua'))()
```

### Window

```lua
local Window =
        Library:CreateWindow(
        {
            Title = "Linoria Lib",
            Center = true,
            AutoShow = true
        }
    )
```

### Tab

```lua
local Tabs = {
        Main = Window:AddTab("Test")
}
```

### Sector

```lua
local Test = Tabs.Test:AddLeftGroupbox("Test")
```

### Button

```lua
Test:AddButton(
    "Test",
    function()
          <--- Add Your Loadstring script here
    end
)
```

### Toggle

```lua
Test:AddToggle(
        "Toggle Test",
        {
            Text = "Enable Test",
            Default = true,
            Tooltip = "Enable",
            Callback = function(State) 
                  
            end 
        }
    )
```

### Dropdown

```lua
Test:AddDropdown(
         "Bruh",
        {
            Values = {"1", "2", "3", "4"}, -- u can add more 
            Default = 1,
            Multi = false,
            Text = "JustBruh",
            Tooltip = "Choose the hit part",
            Callback = function(Pick)
                
            end
        }
    )
```

### Slider

```lua
Test:AddSlider(
    "Slider",
    {
        Text = "Skibidi Sigma",
        Default = 0,
        Min = 0,
        Max = 150,
        Rounding = 1,
        Compact = false,
        Callback = function(Value)
            
        end
    }
)
```

### Other things or etc [config,Watermark]
```lua
Library:SetWatermarkVisibility(true)

-- Example of dynamically-updating watermark with common traits (fps and ping)
local FrameTimer = tick()
local FrameCounter = 0;
local FPS = 60;

local WatermarkConnection = game:GetService('RunService').RenderStepped:Connect(function()
    FrameCounter += 1;

    if (tick() - FrameTimer) >= 1 then
        FPS = FrameCounter;
        FrameTimer = tick();
        FrameCounter = 0;
    end;

    Library:SetWatermark(('Nexo.lua | %s fps | %s ms'):format(
        math.floor(FPS),
        math.floor(game:GetService('Stats').Network.ServerStatsItem['Data Ping']:GetValue())
    ));
end);

Library.KeybindFrame.Visible = true; -- todo: add a function for this

Library:OnUnload(function()
    WatermarkConnection:Disconnect()

    print('Unloaded!')
    Library.Unloaded = true
end)

-- UI Settings
local MenuGroup = Tabs['UI Settings']:AddLeftGroupbox('Menu')

-- I set NoUI so it does not show up in the keybinds menu
MenuGroup:AddButton('Unload', function() Library:Unload() end)
MenuGroup:AddLabel('Menu bind'):AddKeyPicker('MenuKeybind', { Default = 'End', NoUI = true, Text = 'Menu keybind' })

Library.ToggleKeybind = Options.MenuKeybind -- Allows you to have a custom SaveManager:IgnoreThemeSettings()

-- Adds our MenuKeybind to the ignore list
-- (do you want each config to have a different menu key? probably not.)
-- SaveManager:SetIgnoreIndexes({ 'MenuKeybind' })

ThemeManager:SetLibrary(Library)
SaveManager:SetLibrary(Library)

SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({ 'MenuKeybind' })

ThemeManager:SetFolder('Nexolua')
SaveManager:SetFolder('Nexolua/configs')

SaveManager:BuildConfigSection(Tabs['UI Settings'])
ThemeManager:ApplyToTab(Tabs['UI Settings'])

SaveManager:LoadAutoloadConfig()

```

