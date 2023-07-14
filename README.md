# Define una aplicación de manera declarativa utilizando un archivo YAML.

1. Aplica el archivo
    
    ```bash
    kubectl apply -f application.yaml
    ```
    
2. Sincroniza la aplicación y verifica que los recursos se crearon en el clúster de destino.

Explicación:

**`apiVersion: argoproj.io/v1alpha1`**: Especifica la versión de la API de Argo CD utilizada en el manifiesto.

- **`kind: Application`**: Define que se trata de una aplicación en Argo CD.
- **`metadata`**: Contiene metadatos asociados a la aplicación, como el nombre y el espacio (namespace) en el que se creará.
    - **`name: microbot-application`**: Es el nombre asignado a la aplicación.
    - **`namespace: argocd`**: Es el espacio (namespace) en el que se creará la aplicación.
- **`spec`**: Especifica la configuración de la aplicación.
    - **`destination`**: Indica la ubicación de implementación de la aplicación.
        - **`namespace: microbot`**: Especifica el espacio (namespace) de Kubernetes donde se desplegará la aplicación.
        - **`server: "https://kubernetes.default.svc"`**: Especifica la dirección del servidor de Kubernetes donde se desplegará la aplicación.
    - **`project: default`**: Especifica el proyecto de Argo CD al que pertenece la aplicación.
    - **`source`**: Indica la fuente del código y las revisiones a utilizar para la implementación.
        - **`path: .`**: Especifica la ruta del repositorio donde se encuentra el código de la aplicación (en este caso, el directorio actual).
        - **`repoURL: "https://github.com/germanmgarcia/microbot_minikube"`**: Es la URL del repositorio de Git donde se encuentra el código de la aplicación.
        - **`targetRevision: main`**: Especifica la revisión o rama del repositorio que se utilizará para la implementación (en este caso, la rama "main").
    - **`syncPolicy`**: Define la política de sincronización de la aplicación.
        - **`syncOptions`**: Permite configurar opciones adicionales de sincronización.
            - **`CreateNamespace=true`**: Indica que se debe crear el espacio (namespace) especificado en la sección **`destination`** si no existe.