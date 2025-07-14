<!DOCTYPE html>
<html lang="es-MX">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CFE INVENTARIO | Sistema de Gestión</title>
    
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Estilos personalizados -->
    <style>
        :root {
            --cfe-primary: #003366;
            --cfe-primary-light: #0066cc;
            --cfe-secondary: #2D7DD2;
            --cfe-accent: #FFCC00;
            --cfe-light: #F5F5F5;
            --cfe-dark: #333333;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f8f9fa;
        }
        
        .navbar-cfe {
            background-color: var(--cfe-primary);
        }
        
        .navbar-cfe .navbar-brand {
            color: white;
            font-weight: bold;
        }
        
        .navbar-cfe .nav-link {
            color: rgba(255, 255, 255, 0.85);
        }
        
        .navbar-cfe .nav-link:hover {
            color: var(--cfe-accent);
        }
        
        .card-cfe {
            border: none;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }
        
        .card-cfe:hover {
            transform: translateY(-5px);
        }
        
        .card-header-cfe {
            background-color: var(--cfe-primary);
            color: white;
            border-radius: 10px 10px 0 0 !important;
        }
        
        .bg-gradient-primary {
            background: linear-gradient(135deg, var(--cfe-primary), var(--cfe-primary-light)) !important;
        }
        
        .bg-gradient-success {
            background: linear-gradient(135deg, #28a745, #218838) !important;
        }
        
        .bg-gradient-info {
            background: linear-gradient(135deg, #17a2b8, #138496) !important;
        }
        
        .btn-cfe {
            background-color: var(--cfe-primary);
            color: white;
        }
        
        .btn-cfe:hover {
            background-color: var(--cfe-primary-light);
            color: white;
        }
        
        .list-group-item {
            transition: background-color 0.3s;
        }
        
        .list-group-item:hover {
            background-color: rgba(0, 87, 63, 0.05);
        }
        
        .alert {
            border-left: 4px solid transparent;
            border-radius: 0.375rem;
        }
        
        .alert-primary {
            border-left-color: var(--cfe-primary);
        }
        
        .alert-success {
            border-left-color: #28a745;
        }
        
        .alert-info {
            border-left-color: #17a2b8;
        }
        
        .alert-danger {
            border-left-color: #dc3545;
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
                <div class="card card-cfe">
                    <div class="card-header card-header-cfe">
                        <h5 class="mb-0"><i class="fas fa-bars mr-2"></i>Menú Principal</h5>
                    </div>
                    <div class="list-group list-group-flush">
                        <a href="#" class="list-group-item list-group-item-action active">
                            <i class="fas fa-tachometer-alt mr-2"></i>Dashboard
                        </a>
                        <a href="#" class="list-group-item list-group-item-action">
                            <i class="fas fa-boxes mr-2"></i>Artículos
                        </a>
                        <a href="#" class="list-group-item list-group-item-action">
                            <i class="fas fa-tags mr-2"></i>Categorías
                        </a>
                        <a href="#" class="list-group-item list-group-item-action">
                            <i class="fas fa-warehouse mr-2"></i>Almacenes
                        </a>
                        <a href="#" class="list-group-item list-group-item-action">
                            <i class="fas fa-truck mr-2"></i>Proveedores
                        </a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-9">
                <!-- Notificaciones -->
                <div class="row mb-4">
                    <div class="col-12">
                        @if (session('status'))
                            <div class="alert alert-success alert-dismissible fade show shadow-sm" role="alert">
                                <div class="d-flex align-items-center">
                                    <i class="fas fa-check-circle mr-3"></i>
                                    <div>{{ session('status') }}</div>
                                </div>
                                <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
                            </div>
                        @endif

                        @if (session('error'))
                            <div class="alert alert-danger alert-dismissible fade show shadow-sm" role="alert">
                                <div class="d-flex align-items-center">
                                    <i class="fas fa-exclamation-circle mr-3"></i>
                                    <div>{{ session('error') }}</div>
                                </div>
                                <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
                            </div>
                        @endif

                        {{-- Mensaje personalizado según rol --}}
                        @role('admin')
                        <div class="alert alert-primary shadow-sm">
                            <div class="d-flex align-items-center">
                                <i class="fas fa-user-shield mr-3 fa-lg"></i>
                                <div>
                                    <strong>Bienvenido administrador.</strong>
                                    <div class="small mt-1">Tienes acceso completo al sistema.</div>
                                </div>
                            </div>
                        </div>
                        @elserole('encargado')
                        <div class="alert alert-success shadow-sm">
                            <div class="d-flex align-items-center">
                                <i class="fas fa-user-cog mr-3 fa-lg"></i>
                                <div>
                                    <strong>Bienvenido encargado.</strong>
                                    <div class="small mt-1">Buen trabajo, gestiona los recursos eficientemente.</div>
                                </div>
                            </div>
                        </div>
                        @elserole('empleado')
                        <div class="alert alert-info shadow-sm">
                            <div class="d-flex align-items-center">
                                <i class="fas fa-user mr-3 fa-lg"></i>
                                <div>
                                    <strong>Bienvenido empleado.</strong>
                                    <div class="small mt-1">Solo podrás ver tus recursos asignados.</div>
                                </div>
                            </div>
                        </div>
                        @endrole
                    </div>
                </div>

                <!-- Panel principal -->
                <div class="card card-cfe mb-4">
                    <div class="card-header card-header-cfe">
                        <div class="d-flex justify-content-between align-items-center">
                            <h4 class="mb-0 text-white">
                                <i class="fas fa-bolt mr-2"></i>
                                Sistema de Inventario CFE
                            </h4>
                        </div>
                    </div>

                    <div class="card-body">
                        <!-- Tarjetas de módulos -->
                        <div class="row">
                            <!-- Tarjeta de Movimientos -->
                            <div class="col-md-4 mb-4">
                                <div class="card card-cfe h-100">
                                    <div class="card-header card-header-cfe bg-gradient-primary">
                                        <h5 class="mb-0 text-white"><i class="fas fa-exchange-alt mr-2"></i>Movimientos</h5>
                                    </div>
                                    <div class="card-body">
                                        <ul class="list-group list-group-flush">
                                            <li class="list-group-item border-0 px-0 py-2">
                                                <a href="prestamos" class="d-flex align-items-center text-decoration-none text-dark">
                                                    <i class="fas fa-hand-holding mr-3 text-primary"></i>
                                                    <span>Préstamos</span>
                                                    <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                                </a>
                                            </li>

                                            @role('admin|encargado')
                                            @if (!auth()->user()->hasRole('empleado'))
                                                <li class="list-group-item border-0 px-0 py-2">
                                                    <a href="ingresos" class="d-flex align-items-center text-decoration-none text-dark">
                                                        <i class="fas fa-sign-in-alt mr-3 text-primary"></i>
                                                        <span>Ingresos</span>
                                                        <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                                    </a>
                                                </li>
                                            @endif
                                            @endrole
                                        </ul>
                                    </div>
                                </div>
                            </div>

                            <!-- Tarjeta de Materiales -->
                            <div class="col-md-4 mb-4">
                                <div class="card card-cfe h-100">
                                    <div class="card-header card-header-cfe bg-gradient-success">
                                        <h5 class="mb-0 text-white"><i class="fas fa-boxes mr-2"></i>Materiales</h5>
                                    </div>
                                    <div class="card-body">
                                        @role('admin|encargado')
                                        <ul class="list-group list-group-flush">
                                            @if (!auth()->user()->hasRole('empleado'))
                                                <li class="list-group-item border-0 px-0 py-2">
                                                    <a href="almacens" class="d-flex align-items-center text-decoration-none text-dark">
                                                        <i class="fas fa-warehouse mr-3 text-success"></i>
                                                        <span>Almacenes</span>
                                                        <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                                    </a>
                                                </li>
                                            @endif
                                        @endrole

                                            <li class="list-group-item border-0 px-0 py-2">
                                                <a href="materials" class="d-flex align-items-center text-decoration-none text-dark">
                                                    <i class="fas fa-box-open mr-3 text-success"></i>
                                                    <span>Materiales</span>
                                                    <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                                </a>
                                            </li>

                                            @role('admin|encargado')
                                            @if (!auth()->user()->hasRole('empleado'))
                                                <li class="list-group-item border-0 px-0 py-2">
                                                    <a href="stocks" class="d-flex align-items-center text-decoration-none text-dark">
                                                        <i class="fas fa-clipboard-list mr-3 text-success"></i>
                                                        <span>Stocks</span>
                                                        <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                                    </a>
                                                </li>
                                            @endif
                                            @endrole
                                        </ul>
                                    </div>
                                </div>
                            </div>

                            @role('admin|encargado')
                            @if (!auth()->user()->hasRole('empleado'))
                                <div class="col-md-4 mb-4">
                                    <div class="card card-cfe h-100">
                                        <div class="card-header card-header-cfe bg-gradient-info">
                                            <h5 class="mb-0 text-white"><i class="fas fa-tags mr-2"></i>Administración</h5>
                                        </div>
                                        <div class="card-body">
                                            <ul class="list-group list-group-flush">
                                                <li class="list-group-item border-0 px-0 py-2">
                                                    <a href="users" class="d-flex align-items-center text-decoration-none text-dark">
                                                        <i class="fas fa-users mr-3 text-info"></i>
                                                        <span>Usuarios</span>
                                                        <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                                    </a>
                                                </li>
                                            </ul>
                                        </div>
                                    </div>
                                </div>
                            @endif
                            @endrole
                        </div>

                        <!-- Información adicional -->
                        <div class="row mt-4 pt-3 border-top">
                            <div class="col-md-6">
                                <div class="d-flex align-items-center p-3 bg-light rounded">
                                    <i class="fas fa-question-circle fa-2x text-primary mr-3"></i>
                                    <div>
                                        <h6 class="mb-1">¿Necesitas ayuda?</h6>
                                        <p class="small text-muted mb-0">Consulta el manual de usuario o contacta al administrador.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
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
