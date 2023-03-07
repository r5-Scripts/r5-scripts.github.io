[qb-core / server / functions.lua](https://github.com/qbcore-framework/qb-core/blob/main/server/functions.lua)  

## Player

### `GetCoords()`
:   Returns the coordinates of any entity.
    ```lua
    QBCore.Functions.GetCoords(entity)
    ```

    - `entity` `(number)` - The entity you wish to get the coords of
    - returns `vector4`

    ```lua title="Usage Example" linenums="1"
    local ped = GetPlayerPed(source)
    local coords = QBCore.Functions.GetCoords(ped)
    print(coords)
    ```

### `GetIdentifier()`
:   Returns the requested `identifier` type for the requested `source`.
    ```lua
    QBCore.Functions.GetIdentifier(source, idtype)
    ```

    - `source` `(any)` - The source to get identifier of
    - `idtype` `(string)` - The identifier type
    - returns `string` | `nil`

    ```lua title="Usage Example" linenums="1"
    local identifier = QBCore.Functions.GetIdentifier(source, 'license')
    print(identifier)

    -- OR: defaults to the identifier in the config of qb-core
    local identifier = QBCore.Functions.GetIdentifier(source)
    print(identifier)
    ```

### `GetSource()`
:   Returns a players `source` by `identifer`
    ```lua
    QBCore.Functions.GetSource(identifier)
    ```

    - `identifier` `(string)` - The identifer of target source
    - returns `number` | `0`

    ```lua title="Usage Example" linenums="1"
    local identifier = QBCore.Functions.GetIdentifier(source, 'license')
    local playerSource = QBCore.Functions.GetSource(identifier)
    print(playerSource)
    ```

### `GetPlayer()`
:   Returns the `player` class instance for a given `source`.
    ```lua
    QBCore.Functions.GetPlayer(source)
    ```

    - `source` `(any)` - The player source
    - returns `table` | `nil`

    ```lua title="Usage Example" linenums="1"
    local Player = QBCore.Functions.GetPlayer(source)
    print(QBCore.Debug(Player))

    -- OR access some player data
    local Player = QBCore.Functions.GetPlayer(source)
    print(Player.PlayerData.citizenid)
    ```

### `GetPlayerByCitizenId()`
:   Returns the `player` class instance for a given `citizenid`.
    ```lua
    QBCore.Functions.GetPlayerByCitizenId(citizenid)
    ```

    - `citizenid` `(string)` - The citizen id
    - returns `table` | `nil`

    ```lua title="Usage Example" linenums="1"
    local Player = QBCore.Functions.GetPlayerByCitizenId('ONZ55343')
    print(QBCore.Debug(Player))

    -- OR access some player data
    local Player = QBCore.Functions.GetPlayerByCitizenId('ONZ55343')
    print(Player.PlayerData.license)
    ```

### `GetOfflinePlayerByCitizenId()`
:   Get an offline player object for a given citizen id.
    ```lua
    QBCore.Functions.GetOfflinePlayerByCitizenId(citizenid)
    ```

    - `citizenid` `(string)` - The citizen id
    - returns `table` | `nil`

    ```lua title="Usage Example" linenums="1"
    local Player = QBCore.Functions.GetOfflinePlayerByCitizenId('ONZ55343')
    print(QBCore.Debug(Player))

    -- OR access some player data
    local Player = QBCore.Functions.GetOfflinePlayerByCitizenId('ONZ55343')
    print(Player.PlayerData.license)
    ```

### `GetPlayerByPhone()`
:   Get the player object from their phone number
    ```lua
    QBCore.Functions.GetPlayerByPhone(number)
    ```

    - `number` `(string)` - The phone number
    - returns `table` | `nil`

    ```lua title="Usage Example" linenums="1"
    local Player = QBCore.Functions.GetPlayerByPhone('12345')
    print(QBCore.Debug(Player))

    -- OR access some player data
    local Player = QBCore.Functions.GetPlayerByPhone('12345')
    print(Player.PlayerData.license)
    ```

### `GetPlayers()`
:   Get a list of player sources
    ```lua
    QBCore.Functions.GetPlayers()
    ```

    - returns `table`

    ```lua title="Usage Example" linenums="1"
    local Players = QBCore.Functions.GetPlayers()
    print(QBCore.Debug(Players))
    ```

### `GetQBPlayers()`
:   Will return an array of QB Player class instances, unlike the `GetPlayers()` wrapper which only returns IDs
    ```lua
    QBCore.Functions.GetQBPlayers()
    ```

    - returns `table`

    ```lua title="Usage Example" linenums="1"
    local Players = QBCore.Functions.GetQBPlayers()
    print(QBCore.Debug(Players))
    ```

### `GetPlayersOnDuty()`
:   Gets a list of all on duty `players` of a specified job and the `count`
    ```lua
    QBCore.Functions.GetPlayersOnDuty(job)
    ```

    - `job` `(string)` - The specified job
    - returns `table`, `number`

### `GetDutyCount()`
:   Returns the amount of players on duty for the specified `job`
    ```lua
    QBCore.Functions.GetDutyCount(job)
    ```

    - `job` `(string)` - The specified job
    - returns `number`

## Routing Buckets
Functions relating to the use of `routing buckets`

!!! info "Learn more about Routing Buckets"
    Server versions from pipeline ID 3245 and above have added a ‘routing bucket’ functionality, which is similar in concept to the ‘dimension’ or ‘virtual world’ functionality seen in prior non-Rockstar GTA network implementations.

    [Read more...](https://cookbook.fivem.net/2020/11/27/routing-buckets-split-game-state/)

### `GetBucketObjects()`
:   Get the routing bucket objects. Returns a table of `player_buckets` and `entity_buckets`
    ```lua
    QBCore.Functions.GetBucketObjects()
    ```

    - returns `table`, `table`

### `SetPlayerBucket()`
:   Will set the provided player id / source into the provided bucket id.  
    Returns `true` if successful
    ```lua
    QBCore.Functions.SetPlayerBucket(source, bucket)
    ```

    - `source` `(number)` - The player source
    - `bucket` `(number)` - The routing bucket to set the player to
    - returns `boolean`

### `SetEntityBucket()`
:   Will set any entity into the provided bucket, for example peds / vehicles / props / etc.  
    Returns `true` if successful.
    ```lua
    QBCore.Functions.SetEntityBucket(entity, bucket)
    ```

    - `entity` `(number)` - The entity
    - `bucket` `(number)` - The routing bucket to set the entity to
    - returns `boolean`

### `GetPlayersInBucket()`
:   Will return an array of all the player ids inside the current bucket
    ```lua
    QBCore.Functions.GetPlayersInBucket(bucket)
    ```

    - `bucket` `(number)` - The routing bucket
    - returns `table` | `false`

### `GetEntitiesInBucket()`
:   Will return an array of all the entities inside the current bucket (not for player entities, use GetPlayersInBucket for that)
    ```lua
    QBCore.Functions.GetEntitiesInBucket(bucket)
    ```

    - `bucket` `(number)` - The routing bucket
    - returns `table` | `false`

## Vehicles
### `SpawnVehicle()`
:   Server side vehicle creation with optional callback.
    The `CreateVehicle` RPC still uses the client for creation so players must be near
    ```lua
    QBCore.Functions.SpawnVehicle(source, model, coords, warp)
    ```

    - `source` `(number)` - The player source. This player will be set as the entity owner.
    - `model` `(string | hash)` - The vehicle model.
    - `coords?` `(vector3)` - (optional) The spawn location. Defaults to the player position if not given.
    - `warp?` `boolean` - (optional) Will warp the player inside the vehicle if `true`.
    - returns `veh` - A script handle (fwScriptGuid index) for the vehicle, or 0 if the vehicle failed to be created.

    ```lua title="Usage Example" linenums="1"
    QBCore.Functions.CreateCallback('qb-garage:server:spawnvehicle', function (source, cb, vehInfo, coords, warp)
        local plate = vehInfo.plate
        local veh = QBCore.Functions.SpawnVehicle(source, vehInfo.vehicle, coords, warp)
        SetEntityHeading(veh, coords.w)
        SetVehicleNumberPlateText(veh, plate)
        local vehProps = {}
        local result = MySQL.query.await('SELECT mods FROM player_vehicles WHERE plate = ?', {plate})
        if result[1] then vehProps = json.decode(result[1].mods) end
        local netId = NetworkGetNetworkIdFromEntity(veh)
        OutsideVehicles[plate] = {netID = netId, entity = veh}
        cb(netId, vehProps)
    end)
    ```

### `CreateVehicle()`
:   Server side vehicle creation with optional callback.  
    The CreateAutomobile native is still experimental but doesn't use client for creation. This doesn't work for all vehicles!
    ```lua
    QBCore.Functions.CreateVehicle(source, model, coords, warp)
    ```

    - `source` `(number)` - The player source. This player will be set as the entity owner.
    - `model` `(string | hash)` - The vehicle model.
    - `coords?` `(vector3)` - (optional) The spawn location. Defaults to the player position if not given.
    - `warp?` `boolean` - (optional) Will warp the player inside the vehicle if `true`.
    - returns `veh` - A script handle (fwScriptGuid index) for the vehicle, or 0 if the vehicle failed to be created.

## Callbacks

### `TriggerClientCallback()`
:   Triggersa client-side callback from server-side script.
    ```lua
    QBCore.Functions.TriggerClientCallback(name, source, cb, ...)
    ```

    - `name` `(string)` - The callback name
    - `source` `(number)` - The source player
    - `cb` `(function)` - The callback function
    - `...` `(any)` - Additional parameters for the callback function

### `CreateCallback()`
:   Create a server-side callback function
    ```lua
    QBCore.Functions.CreateCallback(name, cb)
    ```

    - `name` `(string)` - The callback name
    - `cb` `(function)` - The callback function

### `TriggerCallback()`
:   Trigger a server-side callback from a server-side script.
    ```lua
    QBCore.Functions.TriggerCallback(name, source, cb, ...)
    ```

    - `name` `(string)` - The callback name
    - `source` `(number)` - The source player
    - `cb` `(function)` - The callback function
    - `...` `(any)` - Additional parameters for the callback function

## Items

### `CreateUsableItem()`
:   Create a usable item and define its function.
    ```lua
    QBCore.Functions.CreateUseableItem(item, data)
    ```

    - `item` `(string)` - The item name
    - `data` `(function)` -  The item callback function

    ```lua title="Usage Example" linenums="1"
    QBCore.Functions.CreateUseableItem("joint", function(source, item)
        local Player = QBCore.Functions.GetPlayer(source)
        if not Player.Functions.RemoveItem(item.name, 1, item.slot) then return end
        TriggerClientEvent("consumables:client:UseJoint", source)
    end)
    ```

### `CanUseItem()`
:   Check if an item is usable.
    ```lua
    QBCore.Functions.CanUseItem(item)
    ```

    - `item` `(string)` - The item name
    - returns `function` | `nil`

### `UseItem()`
:   Use an item on the player.
    !!! warning "Requires `qb-inventory`"
    ```lua
    QBCore.Functions.UseItem(source, item)
    ```

    - `source` `(number)` - The player source
    - `item` `(string)` - The item name

### `HasItem()`
:   Check if the player has an item of a given amount.
    !!! warning "Requires `qb-inventory`"
    ```lua
    QBCore.Functions.HasItem(source, items, amount)
    ```

    - `source` `(number)` - The player source
    - `items` `(string | table)` - The item(s) required
    - `amount` `(number)` - The amount required
    - returns `boolean`

## Server Administration

### `Kick()`
:   Kick a player from the server
    ```lua
    QBCore.Functions.Kick(source, reason, setKickReason, deferrals)
    ```

    - `source` `(number)` - The player source
    - `reason` `(string)` - The reason for kick
    - `setKickReason` `(boolean)` - Whether to set the kick reason or not
    - `deferrals` `(boolean)` - Whether to update the deferrals messages or not

### `IsWhitelisted()`
:   Check if a player is whitelisted.
    ```lua
    QBCore.Functions.IsWhitelisted(source)
    ```

    - `source` `(number)` - The player source
    - returns `boolean`

### `AddPermission()`
:   Add an ace permission to a player. This will only register for the current session. For persistent permissions, refer to [Setting Permissions](#).
    ```