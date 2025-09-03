import 'package:flutter/material.dart';

void main() {
  runApp(const MainApp());
}

class MainApp extends StatelessWidget {
  const MainApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // Desactiva la cinta de "Debug" en la esquina
      debugShowCheckedModeBanner: false,
      title: 'MIS CONTACTOS',
      theme: ThemeData(
        useMaterial3: true,
        // Color base para generar la paleta de colores de la app
        colorSchemeSeed: Colors.blue,
      ),
      home: const ProfileScreen(),
    );
  }
}

class ProfileScreen extends StatelessWidget {
  const ProfileScreen({
    super.key,
  });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.grey[200],
      appBar: AppBar(
        title: const Text('MIS CONTACTOS'),
        backgroundColor: Colors.blue[800],
        foregroundColor: Colors.white,
      ),
      body: const Center(
        child: ProfileCard(),
      ),
    );
  }
}

class ProfileCard extends StatelessWidget {
  const ProfileCard({
    super.key,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: const EdgeInsets.all(20),
      child: Card(
        elevation: 8,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(15),
        ),
        // Wrap the content in SingleChildScrollView to prevent overflow
        child: SingleChildScrollView(
          child: Padding(
            padding: const EdgeInsets.all(24),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                // Foto de perfil, changed to NetworkImage as per instructions
                const CircleAvatar(
                  radius: 50,
                  backgroundImage: NetworkImage(
                      'https://www.gstatic.com/flutter-onestack-prototype/genui/example_1.jpg'),
                ),
                const SizedBox(height: 20),

                // Nombre actualizado
                const Text(
                  'Luis Cartagena',
                  style: TextStyle(
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                    color: Colors.black87,
                  ),
                ),
                const SizedBox(height: 8),

                // Email actualizado
                Text(
                  'cartagenaluis58@gmail.com',
                  style: TextStyle(
                    fontSize: 16,
                    color: Colors.grey[700],
                  ),
                ),
                const SizedBox(height: 24),

                // Fila de botones de contacto
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    ElevatedButton.icon(
                      onPressed: () {
                        _mostrarMensaje(context, 'Llamando a Luis...');
                      },
                      icon: const Icon(Icons.phone),
                      label: const Text('Llamar'),
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.blue,
                        foregroundColor: Colors.white,
                      ),
                    ),
                    ElevatedButton.icon(
                      onPressed: () {
                        _mostrarMensaje(context, 'Enviando mensaje...');
                      },
                      icon: const Icon(Icons.message),
                      label: const Text('Mensaje'),
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.green,
                        foregroundColor: Colors.white,
                      ),
                    ),
                  ],
                ),
                const SizedBox(height: 18),

                // Botón de editar perfil
                SizedBox(
                  width: double.infinity,
                  child: ElevatedButton.icon(
                    onPressed: () {
                      _mostrarMensaje(context, 'Abriendo editor de perfil...');
                    },
                    icon: const Icon(Icons.edit),
                    label: const Text('Editar perfil'),
                    style: ElevatedButton.styleFrom(
                      backgroundColor: Colors.black54,
                      foregroundColor: Colors.white,
                      padding: const EdgeInsets.symmetric(vertical: 12),
                    ),
                  ),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }

  // Función para mostrar mensajes en un SnackBar
  void _mostrarMensaje(BuildContext context, String mensaje) {
    // Oculta cualquier SnackBar anterior antes de mostrar uno nuevo
    ScaffoldMessenger.of(context).hideCurrentSnackBar();
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(
        content: Text(mensaje),
        duration: const Duration(seconds: 3),
        backgroundColor: Colors.blue[800],
      ),
    );
  }
}
