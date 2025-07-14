<!DOCTYPE html>
<html lang="es-MX">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CFE INVENTARIO | Sistema de Gestión</title>
    
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    
    <!-- Estilos personalizados -->
    <style>
        :root {
            --cfe-blue: #003366;
            --cfe-light-blue: #0066cc;
            --cfe-yellow: #ffcc00;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f8f9fa;
        }
        
        .navbar-cfe {
            background-color: var(--cfe-blue);
        }
        
        .navbar-cfe .navbar-brand {
            color: white;
            font-weight: bold;
        }
        
        .navbar-cfe .nav-link {
            color: rgba(255, 255, 255, 0.85);
        }
        
        .navbar-cfe .nav-link:hover {
            color: var(--cfe-yellow);
        }
        
        .card-header-cfe {
            background-color: var(--cfe-light-blue);
            color: white;
        }
        
        .btn-cfe {
            background-color: var(--cfe-blue);
            color: white;
        }
        
        .btn-cfe:hover {
            background-color: var(--cfe-light-blue);
            color: white;
        }
    </style>
</head>
<body>
    <!-- Barra de navegación -->
    <nav class="navbar navbar-expand-lg navbar-dark navbar-cfe shadow-sm">
        <div class="container">
            <a class="navbar-brand" href="#">
                <img src="assets/img/logo-cfe.png" alt="CFE" height="40" class="d-inline-block align-top me-2">
                INVENTARIO
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link" href="#">Inicio</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Inventario</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Reportes</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Usuarios</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Contenido principal -->
    <main class="container my-5">
        <div class="row">
            <div class="col-md-3">
                <!-- Sidebar -->
                <div class="card shadow-sm">
                    <div class="card-header card-header-cfe">
                        Menú Principal
                    </div>
                    <div class="list-group list-group-flush">
                        <a href="#" class="list-group-item list-group-item-action active">Dashboard</a>
                        <a href="#" class="list-group-item list-group-item-action">Artículos</a>
                        <a href="#" class="list-group-item list-group-item-action">Categorías</a>
                        <a href="#" class="list-group-item list-group-item-action">Almacenes</a>
                        <a href="#" class="list-group-item list-group-item-action">Proveedores</a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-9">
                <!-- Contenido dinámico -->
                <div class="card shadow-sm">
                    <div class="card-header card-header-cfe d-flex justify-content-between align-items-center">
                        <h5 class="mb-0">@yield('title', 'Dashboard')</h5>
                        @yield('header-actions')
                    </div>
                    <div class="card-body">
                        @yield('content')
                        
                        <!-- Ejemplo de contenido -->
                        <h1 class="display-4">Bienvenido al Sistema de Inventario CFE</h1>
                        <p class="lead">Gestión completa de activos y materiales</p>
                        <hr class="my-4">
                        <p>Seleccione una opción del menú para comenzar.</p>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- Pie de página -->
    <footer class="bg-dark text-white py-4 mt-5">
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <h5>CFE INVENTARIO</h5>
                    <p>Sistema de gestión de inventarios para la Comisión Federal de Electricidad</p>
                </div>
                <div class="col-md-3">
                    <h5>Enlaces</h5>
                    <ul class="list-unstyled">
                        <li><a href="#" class="text-white">Acerca de</a></li>
                        <li><a href="#" class="text-white">Contacto</a></li>
                        <li><a href="#" class="text-white">Políticas</a></li>
                    </ul>
                </div>
                <div class="col-md-3">
                    <h5>Soporte</h5>
                    <ul class="list-unstyled">
                        <li><a href="#" class="text-white">Documentación</a></li>
                        <li><a href="#" class="text-white">Reportar problema</a></li>
                    </ul>
                </div>
            </div>
            <hr>
            <div class="text-center">
                <p class="mb-0">© 2023 Comisión Federal de Electricidad. Todos los derechos reservados.</p>
            </div>
        </div>
    </footer>

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    
    <!-- Scripts personalizados -->
    <script>
        // Aquí puedes agregar tu lógica JavaScript
        document.addEventListener('DOMContentLoaded', function() {
            console.log('Sistema CFE INVENTARIO cargado');
            
            // Lógica para manejar la autenticación
            @unless(request()->is('/') || request()->is('login') || request()->is('register'))
                @php
                    $user = auth()->user();
                    $isEmbedded = $user->hasRole('embedded');
                @endphp
            @endunless
        });
    </script>
</body>
</html>
