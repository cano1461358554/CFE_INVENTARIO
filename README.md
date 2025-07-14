
<html lang="es-MX">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CFE Sistema de Inventario</title>
    
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Estilos personalizados -->
    <style>
        :root {
            --cfe-primary: #00573F;
            --cfe-primary-light: #007A5E;
            --cfe-secondary: #2D7DD2;
            --cfe-accent: #FFC845;
            --cfe-light: #F5F5F5;
            --cfe-dark: #333333;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f8f9fa;
            padding-top: 70px;
        }

        .navbar-cfe {
            background-color: var(--cfe-primary);
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
        }

        .navbar-brand {
            font-weight: bold;
            font-size: 1.5rem;
        }

        .nav-link {
            color: #FFFFFF !important;
            padding: 10px 15px;
            transition: background-color 0.3s ease;
        }

        .nav-link:hover {
            background-color: #003D2C;
            border-radius: 4px;
        }

        .dropdown-menu {
            background-color: #007A5E;
            border: none;
        }

        .dropdown-item {
            color: #FFFFFF;
        }

        .dropdown-item:hover {
            background-color: #00573F;
        }

        .content {
            padding: 20px;
            background-color: #FFFFFF;
            min-height: calc(100vh - 70px);
        }

        .table {
            border-collapse: separate;
            border-spacing: 0;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .table th {
            background-color: #00573F;
            color: #FFFFFF;
        }

        .table tbody tr:nth-child(even) {
            background-color: #f8f9fa;
        }

        .table tbody tr:hover {
            background-color: #e9ecef;
        }

        .navbar-toggler {
            border-color: rgba(255,255,255,0.5);
        }

        .navbar-toggler-icon {
            background-image: url("data:image/svg+xml;charset=utf8,%3Csvg viewBox='0 0 30 30' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath stroke='rgba(255, 255, 255, 0.8)' stroke-width='2' stroke-linecap='round' stroke-miterlimit='10' d='M4 7h22M4 15h22M4 23h22'/%3E%3C/svg%3E");
        }

        .active-menu-item {
            background-color: #003D2C;
            border-radius: 4px;
        }

        /* Estilos para tarjetas */
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

        /* Estilos para alertas */
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

        /* Estilos para el perfil */
        .profile-overlay {
            position: fixed;
            top: 70px;
            right: -40%;
            width: 40%;
            height: calc(100vh - 70px);
            background-color: white;
            box-shadow: -2px 0 10px rgba(0, 0, 0, 0.1);
            z-index: 999;
            transition: right 0.3s ease;
            overflow-y: auto;
            padding: 20px;
        }

        .profile-overlay.active {
            right: 0;
        }

        .overlay-backdrop {
            position: fixed;
            top: 70px;
            left: 0;
            width: 100%;
            height: calc(100vh - 70px);
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 998;
            display: none;
        }

        .profile-overlay.active ~ .overlay-backdrop {
            display: block;
        }

        .profile-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #eee;
        }

        .profile-header h4 {
            color: #00573F;
            margin: 0;
        }

        .profile-close-btn {
            font-size: 1.2rem;
            color: #6c757d;
        }

        .profile-close-btn:hover {
            color: #00573F;
        }
    </style>
</head>
<body>

<!-- Barra de navegación superior -->
<nav class="navbar navbar-expand-lg navbar-dark navbar-cfe">
    <div class="container">
        <a class="navbar-brand" href="index.html">CFE Inventario</a>

        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarContent">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarContent">
            <ul class="navbar-nav me-auto">
                <!-- Menú Movimientos -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle active-menu-item" href="#" id="movimientosDropdown" data-bs-toggle="dropdown">
                        <i class="fas fa-exchange-alt"></i> Movimientos
                    </a>
                    <div class="dropdown-menu">
                        <a class="dropdown-item active" href="prestamos.html">Préstamos</a>
                        <a class="dropdown-item" href="ingresos.html">Ingresos</a>
                    </div>
                </li>

                <!-- Menú Materiales -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="materialesDropdown" data-bs-toggle="dropdown">
                        <i class="fas fa-boxes"></i> Materiales
                    </a>
                    <div class="dropdown-menu">
                        <a class="dropdown-item" href="materials.html">Materiales</a>
                        <a class="dropdown-item" href="stocks.html">Stocks</a>
                        <a class="dropdown-item" href="almacenes.html">Almacenes</a>
                    </div>
                </li>

                <!-- Menú Administración -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="adminDropdown" data-bs-toggle="dropdown">
                        <i class="fas fa-users-cog"></i> Administración
                    </a>
                    <div class="dropdown-menu">
                        <a class="dropdown-item" href="usuarios.html">Usuarios</a>
                    </div>
                </li>
            </ul>

            <ul class="navbar-nav ms-auto">
                <li class="nav-item">
                    <span class="nav-link text-white">
                        <i class="fas fa-user-tag"></i> Administrador
                    </span>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#" id="showProfile">
                        <i class="fas fa-user-circle"></i> Perfil
                    </a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="login.html">
                        <i class="fas fa-sign-out-alt"></i> Cerrar Sesión
                    </a>
                </li>
            </ul>
        </div>
    </div>
</nav>

<!-- Overlay del Perfil -->
<div class="profile-overlay" id="profileOverlay">
    <div class="profile-header">
        <h4>Perfil de Usuario</h4>
        <button class="profile-close-btn" id="closeProfile">
            <i class="fas fa-times"></i>
        </button>
    </div>
    
    <div class="profile-content">
        <div class="text-center mb-4">
            <img src="assets/img/user-profile.png" alt="Perfil" class="rounded-circle" width="120">
            <h4 class="mt-3">Administrador CFE</h4>
            <p class="text-muted">admin@cfe.gob.mx</p>
        </div>
        
        <div class="list-group">
            <a href="#" class="list-group-item list-group-item-action">
                <i class="fas fa-user-edit mr-2"></i> Editar Perfil
            </a>
            <a href="#" class="list-group-item list-group-item-action">
                <i class="fas fa-lock mr-2"></i> Cambiar Contraseña
            </a>
            <a href="#" class="list-group-item list-group-item-action">
                <i class="fas fa-cog mr-2"></i> Configuración
            </a>
        </div>
    </div>
</div>

<!-- Backdrop para el overlay -->
<div class="overlay-backdrop" id="overlayBackdrop"></div>

<!-- Contenido principal -->
<div class="content">
    <div class="container-fluid">
        <!-- Notificaciones -->
        <div class="row mb-4">
            <div class="col-12">
                <div class="alert alert-primary shadow-sm">
                    <div class="d-flex align-items-center">
                        <i class="fas fa-user-shield mr-3 fa-lg"></i>
                        <div>
                            <strong>Bienvenido administrador.</strong>
                            <div class="small mt-1">Tienes acceso completo al sistema.</div>
                        </div>
                    </div>
                </div>
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
                                        <a href="prestamos.html" class="d-flex align-items-center text-decoration-none text-dark">
                                            <i class="fas fa-hand-holding mr-3 text-primary"></i>
                                            <span>Préstamos</span>
                                            <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                        </a>
                                    </li>
                                    <li class="list-group-item border-0 px-0 py-2">
                                        <a href="ingresos.html" class="d-flex align-items-center text-decoration-none text-dark">
                                            <i class="fas fa-sign-in-alt mr-3 text-primary"></i>
                                            <span>Ingresos</span>
                                            <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                        </a>
                                    </li>
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
                                <ul class="list-group list-group-flush">
                                    <li class="list-group-item border-0 px-0 py-2">
                                        <a href="almacenes.html" class="d-flex align-items-center text-decoration-none text-dark">
                                            <i class="fas fa-warehouse mr-3 text-success"></i>
                                            <span>Almacenes</span>
                                            <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                        </a>
                                    </li>
                                    <li class="list-group-item border-0 px-0 py-2">
                                        <a href="materials.html" class="d-flex align-items-center text-decoration-none text-dark">
                                            <i class="fas fa-box-open mr-3 text-success"></i>
                                            <span>Materiales</span>
                                            <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                        </a>
                                    </li>
                                    <li class="list-group-item border-0 px-0 py-2">
                                        <a href="stocks.html" class="d-flex align-items-center text-decoration-none text-dark">
                                            <i class="fas fa-clipboard-list mr-3 text-success"></i>
                                            <span>Stocks</span>
                                            <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>

                    <!-- Tarjeta de Administración -->
                    <div class="col-md-4 mb-4">
                        <div class="card card-cfe h-100">
                            <div class="card-header card-header-cfe bg-gradient-info">
                                <h5 class="mb-0 text-white"><i class="fas fa-tags mr-2"></i>Administración</h5>
                            </div>
                            <div class="card-body">
                                <ul class="list-group list-group-flush">
                                    <li class="list-group-item border-0 px-0 py-2">
                                        <a href="usuarios.html" class="d-flex align-items-center text-decoration-none text-dark">
                                            <i class="fas fa-users mr-3 text-info"></i>
                                            <span>Usuarios</span>
                                            <i class="fas fa-chevron-right ml-auto text-muted"></i>
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
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

<!-- Scripts -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

<script>
    $(document).ready(function() {
        // Mostrar/ocultar perfil
        $('#showProfile').click(function(e) {
            e.preventDefault();
            $('#profileOverlay').addClass('active');
            $('#overlayBackdrop').show();
        });

        // Cerrar perfil
        $('#closeProfile, #overlayBackdrop').click(function() {
            $('#profileOverlay').removeClass('active');
            $('#overlayBackdrop').hide();
        });

        // Cerrar con tecla ESC
        $(document).keyup(function(e) {
            if (e.key === "Escape") {
                $('#profileOverlay').removeClass('active');
                $('#overlayBackdrop').hide();
            }
        });

        // Manejo de menús activos
        $('.dropdown-item').filter(function() {
            return this.href === window.location.pathname;
        }).addClass('active').closest('.dropdown-menu').prev().addClass('active-menu-item');
    });
</script>

</body>
</html>
