# Configuración de Firebase AngularJs.

Pasos para crear un nuevo.
- Ir a la [Consola de firebase](https://console.firebase.google.com/)
- Ingresar a la opción nuevo proyecto y agregar un nombre al proyecto presionamos continuar, google cloud plataform creara el proyecto y nos re direccionara al dashboard de firebase.
- En la opción configuración del proyecto, deberemos agregar una nueva aplicación ya sea de android, IOS, Web y ahora permite integrarlo con proyectos Unity.
- Una vez agregado proyecto, nos proporcionara el objeto de configuración para poder crear una instancia de firebase en nuestra aplicación obtendremos algo como esto.
- > firebase: {
    apiKey: "AIzaSyCsWbuoeS-H6M-MMs9am1uwuvlMkBb-4sw",
    authDomain: "2323weewwqw.firebaseapp.com",
    databaseURL: "https://app.firebaseio.com",
    projectId: "project-df6e1",
    storageBucket: "project-df6e1.appspot.com",
    messagingSenderId: "6443968228402",
    appId: "1:6443wee9688402:web:b1f127f1943560be55e10b",
    measurementId: "G-F35XNNBPF4"
  }

Una vez creado el proyecto y aplicación en Firebase, tendremos que configurar firebase en nuestra aplicación para ello utilizaremos el manejados de paquetes de node `npm`.

# Pasos de configuración firebase en proyecto angular.

- Instalación de firebase `npm i firebase --dev-save`.
En el archivo enviroments.ts, dentro de la constante `enviroment` agregaremos la configuración que Firebase nos genero al crear la aplicación
- > export const environment = {
  production: false,
  firebase: {
    apiKey: "AIzaSyCsWbuoeS-H6M-MMs9am1uwuvlMkBb-4sw",
    authDomain: "2323weewwqw.firebaseapp.com",
    databaseURL: "https://app.firebaseio.com",
    projectId: "project-df6e1",
    storageBucket: "project-df6e1.appspot.com",
    messagingSenderId: "6443968228402",
    appId: "1:6443wee9688402:web:b1f127f1943560be55e10b",
    measurementId: "G-F35XNNBPF4"
  }
};

- Para finalizar nuestra configuración el archivo module.ts, dentro de la sección de imports agregaremos los modulos de firebase e inyecteremos la configuración que agregmos en el objeto enviroments.
- > imports: [
    AngularFireModule.initializeApp(environment.firebase),
    AngularFireDatabaseModule,
    AngularFirestoreModule,
  ]

Echo esto, estamos listos para iniciar a utilizar los procesos de lectura y escritura del cliente de datos firebase.

- Dentro de un servicio de angular o bien dentro del archivo .ts del componente, importaremos la referencia de Firebase de la siguiente manera.
`import { AngularFirestore } from '@angular/fire/firestore'`
- > @Injectable({
  providedIn: 'root'
})
export class MesasService {
  Collection: string = "Productos"
  constructor(private Context: AngularFirestore) {
  }
}

En el contructor de la clase recibimos el AngularFireStore y estamos listos para empezar a utilizalo, ademas crear una propiedad tipo `string` con el nombre de nuestro documento, en base de datos relacionales las llamda `Tablas`.
# CRUD 
> # Crear 
> /** crea una nueva mesa */
  async crearMesa(mesa: Producto) {
      return await this.Context.collection(this.Collection).add(Producto);
  }

> # Obtener
 > /*Obtiene un documento por Id*/
  async getMesas(Id: string){
    var producto = await this.Context.collection(this.Collection).ref
        .orderBy('Codigo')
        .where("Id", "==", Id)
        .get();
    const data = snapshot.data();
    documents.push({
      id: key,
      ...data
    });
    return documents[0];
  }

  > # Actualizar
 > /*Actualiza un documento */
  async getMesas(producto: Producto){
    return await this.Context.collection(this.Collection).doc(producto.Id).update(producto);
  }


