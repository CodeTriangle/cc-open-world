If you want to contribute to the project, you'll need some basic knowledge of how to read/manipulate JSON, and take a read if you can from [this page](https://wiki.c2dl.info/Patching#Patch_Steps). Can also analyze some of the already existing patches for more info. 
[Example Patch](https://github.com/buanjautista/cc-open-world/blob/main/assets/data/maps/forest/path-10-hidden.json.patch). 
[Another Example Patch](https://github.com/buanjautista/cc-open-world/blob/main/assets/data/maps/jungle/dng/dng-crossing.json.patch).


# What does it do
The way this mod patches work are basically, patches that are added in the same route as the original map thats being replaced (mod://assets/data/maps/..). 
To replace stuff, you need to see on what indexes are the things you want to replace, in the original map. I personally use VSCode to find that info. Make sure the map you're referring to is unedited (no map editor small edits/saves either, since these might change the entities indexes)

## To keep in mind:
- Anything that needs to be removed, will have to be neutralized. Don't remove any entity as it might cause some unexpected behaviors. The way I usually do, is either removing the conditions for events or NPCs to appear, or touching some of the event's flags and variables around to change whatever line needs to be changed. Stuff might still happen but it lessens the chance.
- In case layers or details want to be added for extra stuff (like the autumn's fall into autumn's rise barrier), you have to ADD layers, you cant edit current layers. You might want to try map-editor to fiddle around with new layers, save a extra map, copy the layers and add them as new elements on
- Ideally, try to copy as less code from the game as possible, both for patch space and not take game code :)
- In case you want to comment any of the patch, you can add this line as a patch step, and add the info on your edits there
> "_comment": "Barrier fix so its not tied to story or junglecontinue",



# Useful codes
Example loop to neutralize many events at once:
>{
        "type": "FOR_IN",
        "_comment": "Removes story event triggers",
        "keyword": "__INDEX__",
        "values": [1, 215],
        "body": [{
            "type": "ENTER",
            "index": ["__INDEX__",  "settings"]
        },{
            "type": "SET_KEY",
            "index": "startCondition",
            "content": "false"
        },{
            "type": "EXIT",
            "count": 2
        }]
>},

