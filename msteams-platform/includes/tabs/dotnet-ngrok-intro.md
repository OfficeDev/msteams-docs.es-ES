## <a name="establish-a-secure-tunnel-to-your-tab"></a>Establecer un túnel seguro a la pestaña

Microsoft Teams es un producto basado en la nube completamente y requiere que el contenido de la pestaña esté disponible en la nube con puntos de conexión HTTPS. Teams no permite el hospedaje local. Tendrá que publicar su pestaña en una dirección URL pública o usar un proxy que expondrá el puerto local a una dirección URL accesible desde Internet.

Para probar la pestaña, use [ngrok](https://ngrok.com/docs). Los puntos de conexión web del servidor estarán disponibles mientras se ejecuta ngrok en el equipo local. Si cierra ngrok, las direcciones URL serán distintas la próxima vez que la inicie.