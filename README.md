@page "/"

<PageTitle>Calm Quest</PageTitle>

<div class="text-center mt-5">
    <h1 class="text-primary">🌿 Calm Quest</h1>
    <p class="lead">Tu espacio seguro para expresar lo que sientes 💬</p>
</div>

<div class="card p-4 shadow-lg mt-4">
    <textarea class="form-control mb-3" @bind="mensajeUsuario" placeholder="Escribe aquí cómo te sientes..." rows="4"></textarea>

    <button class="btn btn-success w-100" @onclick="EnviarMensaje">Enviar mensaje ✨</button>

    <div class="mt-4">
        <h5>Consejo de la IA 🧠</h5>
        <p class="alert alert-info">@respuestaIA</p>
    </div>
</div>

<div class="mt-5">
    <h4>📊 Tu progreso emocional</h4>
    <p>Días registrados: @diasRegistrados</p>
    <p>Estado emocional promedio: <b>@estadoPromedio</b></p>
</div>

@code {
    private string mensajeUsuario = "";
    private string respuestaIA = "Escribe algo para que pueda responderte 💬";
    private int diasRegistrados = 0;
    private string estadoPromedio = "Neutral 😊";

    private async Task EnviarMensaje()
    {
        if (string.IsNullOrWhiteSpace(mensajeUsuario))
        {
            respuestaIA = "Cuéntame algo de lo que sientas, estoy aquí para escucharte 🤍";
            return;
        }

        diasRegistrados++;
        respuestaIA = GenerarConsejo(mensajeUsuario);

        // Simular mejora o empeoramiento (estadística sencilla)
        if (mensajeUsuario.Contains("mejor", StringComparison.OrdinalIgnoreCase))
            estadoPromedio = "Mejorando 💚";
        else if (mensajeUsuario.Contains("triste", StringComparison.OrdinalIgnoreCase))
            estadoPromedio = "Triste 😔";
        else if (mensajeUsuario.Contains("ansioso", StringComparison.OrdinalIgnoreCase))
            estadoPromedio = "Ansioso 😟";
        else
            estadoPromedio = "Neutral 😊";

        mensajeUsuario = "";
    }

    private string GenerarConsejo(string texto)
    {
        texto = texto.ToLower();

        if (texto.Contains("ansioso") || texto.Contains("ansiedad"))
            return "Respira profundo. Estás haciendo lo mejor que puedes. Intenta concentrarte en el presente 🌿";

        if (texto.Contains("triste") || texto.Contains("depresión"))
            return "Está bien sentirse mal a veces. Hablar de lo que sientes ya es un paso enorme 🤍";

        if (texto.Contains("feliz") || texto.Contains("mejor"))
            return "¡Qué alegría saber eso! Sigue cuidándote, te mereces sentirte bien 💫";

        return "Gracias por compartirlo. No estás solo, estoy aquí para escucharte 💬";
    }
}
