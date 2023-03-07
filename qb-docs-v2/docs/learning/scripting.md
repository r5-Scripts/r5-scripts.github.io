## Properly Managing PlayerData State Locally
You can use these events to manage local PlayerData state properly. Instead of asking QBCore what your player data is every time something gets called, we just save it locally, and only change it when it gets changed!

You can use this for items tracking as well if you only want to track items instead of the whole playerdata object.

```lua linenums="1"
local QBCore = exports['qb-core']:GetCoreObject()

-- Handles state on resource start (useful for live resource restarts).
-- Will set to empty brackets {} if character not found yet.
local PlayerData = QBCore.Functions.GetPlayerData()

-- Handles state right when the player selects their character and
-- location.
RegisterNetEvent('QBCore:Client:OnPlayerLoaded', function()
    PlayerData = QBCore.Functions.GetPlayerData()
end)

-- Resets state on logout, in case of character change.
RegisterNetEvent('QBCore:Client:OnPlayerUnload', function()
  PlayerData = {}
end)

-- Handles state when PlayerData is changed at all.
RegisterNetEvent('QBCore:Player:SetPlayerData', function(_PlayerData)
    PlayerData = _PlayerData
end)
```

## How to loop through an array
```lua title="How to loop through an array vs object. Difference between pairs and ipairs" linenums="1"
-- Looping through an object table.
-- pairs will NOT stop at the first NIL index
Config.Table = {
    ['a'] = 1,
    ['b'] = 2,
    ['c'] = 3,
}

-- prints a,1 | b,2 | c,2
for key, value in pairs(Config.Table) do
    print(key, value)
end

-- Looping through an array table.
-- ipairs will stop at the first NIL index
Config.Array = { "d", "e", "f" }

-- prints 1,d | 2,e | 3,f
for index, value in ipairs(Config.Array) do
    print(index, value)
end
```