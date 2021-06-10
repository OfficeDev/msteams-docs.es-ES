## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro en la pestaña

Microsoft Teams es un producto totalmente basado en la nube y requiere que el contenido de la pestaña esté disponible desde la nube mediante puntos de conexión HTTPS. Teams no permite el hospedaje local. Deberá publicar la pestaña en una dirección URL pública o usar un proxy que exponga el puerto local a una dirección URL orientada a Internet.

Para probar la pestaña, usará [ngrok](https://ngrok.com/docs). Los puntos de conexión web del servidor estarán disponibles mientras ngrok se ejecuta en el equipo local. Si cierra ngrok, las direcciones URL serán diferentes la próxima vez que la inicie.