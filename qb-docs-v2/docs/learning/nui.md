The first thing to do when new to NUI (short for 'new UI') development is to read the [FiveM documentation](https://docs.fivem.net/docs/scripting-manual/nui-development/).


## Code Snippets

### Client -> UI
```lua title="client.lua" linenums="1"
SendNUIMessage({
    action = "DoSomething",
    data = data
})
```

```lua title="script.js" linenums="1"
window.addEventListener("message", (event) => {
    const data = event.data;
    const action = data.action;

    switch (action) {
        case "DoSomething":
            // Do something
        case "DoNothing":
            // Do nothing
        default:
            return;
    }
});
```

### UI -> Client
```lua title="script.js" linenums="1"
$.post(`https://${GetParentResourceName()}/IDidAThing`,
    JSON.stringify({ data: 'Hi Dad', test: 'This is a test' })
);
```

```lua title="client.lua" linenums="1"
RegisterNUICallback("IDidAThing", function(data, cb)
    print(data.data) -- Hi Dad
    print(data.test) -- This is a test
    cb("ok")
end)
```