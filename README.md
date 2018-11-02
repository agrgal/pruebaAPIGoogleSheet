Probando cómo conectar ANDROID STUDIO a Google Sheet API

1) bibliotecas añadidas en dependencies, build.gradle (app Module)

    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:appcompat-v7:28.0.0'
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'

    // Bibliotecas para conectar con Google Sheet
    implementation 'com.google.android.gms:play-services-auth:16.0.1'
    implementation 'pub.devrel:easypermissions:0.3.0'
    implementation('com.google.api-client:google-api-client-android:1.23.0') {
        exclude group: 'org.apache.httpcomponents'
    }
    implementation('com.google.apis:google-api-services-sheets:v4-rev505-1.23.0') {
        exclude group: 'org.apache.httpcomponents'
    }
    // Faltaba esta biblioteca!!!!!!!!!!!!!!!!!!!!!!!!!!!
    implementation 'com.google.oauth-client:google-oauth-client-jetty:1.23.0'
    // *****************************************************************************

2) Permisos en MANIFEST

    <!--permissions added for spreadsheet v4 api-->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />

3) como recursos, añadido a la carpeta app/src/main/res, está el archivo credentials.json

4) Tras hacer un debug, error en la línea 78-79 del MainActivity.Java, en la clase AppCompatViewInflater.class, 

 public void onClick(@NonNull View v) {
            if (this.mResolvedMethod == null) {
                this.resolveMethod(this.mHostView.getContext(), this.mMethodName);
            }

            try {
                this.mResolvedMethod.invoke(this.mResolvedContext, v);
            } catch (IllegalAccessException var3) {
                throw new IllegalStateException("Could not execute non-public method for android:onClick", var3);
            } catch (InvocationTargetException var4) {
                throw new IllegalStateException("Could not execute method for android:onClick", var4);
            }
        }

Se ejecuta la excepción: ould not execute method for android:onClick"
