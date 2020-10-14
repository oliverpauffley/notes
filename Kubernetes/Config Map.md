# [[Kubernetes]] Config Map
How do you pass config files to pods? like secrets or runtime config files.

You could load them in the application. But that means you need to edit the image and redo the whole thing if the url changes.

Configmaps are external configs that you can change. `DB_URL = mongo.db.service` which can be changed. You can also do secrets in a seperate components.

## Example
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
	name: game-demo
data:
	# property-like keys; each key maps to a value
	player_intial_lives: "3"
	ui_file_name: "user-interface.props"
	
	# file-like keys
	game.properties: | 
		enemy.types=aliens,monsters
		player.maximum_lives=5
```

Then a pod can use the config map as follows:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-demo-pod
spec:
  containers:
    - name: demo
      image: game.example/demo-game
      env:
        # Define the environment variable
        - name: PLAYER_INITIAL_LIVES # Notice that the case is different here
                                     # from the key name in the ConfigMap.
          valueFrom:
            configMapKeyRef:
              name: game-demo           # The ConfigMap this value comes from.
              key: player_initial_lives # The key to fetch.
        - name: UI_PROPERTIES_FILE_NAME
          valueFrom:
            configMapKeyRef:
              name: game-demo
              key: ui_properties_file_name
      volumeMounts:
      - name: config
        mountPath: "/config"
        readOnly: true
  volumes:
    # You set volumes at the Pod level, then mount them into containers inside that Pod
    - name: config
      configMap:
        # Provide the name of the ConfigMap you want to mount.
        name: game-demo
        # An array of keys from the ConfigMap to create as files
        items:
        - key: "game.properties"
          path: "game.properties"
        - key: "user-interface.properties"
          path: "user-interface.properties"
```
