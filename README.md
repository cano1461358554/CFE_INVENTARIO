<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CFE Sistema de Inventario</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f8f9fa;
      padding-top: 70px;
    }

    .navbar-cfe {
      background-color: #00573F;
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

    /* Perfil */
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
      padding: -30px;
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

<!-- NAVBAR (static view only) -->
<nav class="navbar navbar-expand-lg navbar-dark navbar-cfe">
  <div class="container">
    <a class="navbar-brand" href="#">CFE Inventario</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarContent">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarContent">
      <ul class="navbar-nav mr-auto">
        <!-- Menú de ejemplo -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" data-toggle="dropdown">
            <i class="fas fa-exchange-alt"></i> Movimientos
          </a>
          <div class="dropdown-menu">
            <a class="dropdown-item" href="#">Préstamos</a>
            <a class="dropdown-item" href="#">Ingresos</a>
          </div>
        </li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" data-toggle="dropdown">
            <i class="fas fa-boxes"></i> Materiales
          </a>
          <div class="dropdown-menu">
            <a class="dropdown-item" href="#">Materiales</a>
            <a class="dropdown-item" href="#">Stocks</a>
            <a class="dropdown-item" href="#">Almacenes</a>
          </div>
        </li>
      </ul>

      <ul class="navbar-nav ml-auto">
        <li class="nav-item"><a class="nav-link" href="#"><i class="fas fa-user-circle"></i> Perfil</a></li>
        <li class="nav-item"><a class="nav-link" href="#"><i class="fas fa-sign-out-alt"></i> Cerrar Sesión</a></li>
      </ul>
    </div>
  </div>
</nav>

<!-- Contenido principal -->
<div class="content container mt-5">
  <h1 class="mb-4">Sistema de Inventario CFE</h1>
  <p class="lead">Este es un prototipo de interfaz para presentación estática en GitHub Pages.</p>
</div>

<!-- Perfil y Backdrop -->
<div class="profile-overlay" id="profileOverlay">
  <div class="profile-header">
    <h4>Perfil de Usuario</h4>
    <span class="profile-close-btn">&times;</span>
  </div>
  <p class="p-3">Aquí se mostraría la información del usuario.</p>
</div>
<div class="overlay-backdrop" id="overlayBackdrop"></div>

<!-- Scripts -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.min.js"></script>
<script>
  $(document).ready(function () {
    $('#showProfile').click(function (e) {
      e.preventDefault();
      $('#profileOverlay').addClass('active');
    });

    $('#overlayBackdrop, .profile-close-btn').click(function () {
      $('#profileOverlay').removeClass('active');
    });

    $(document).keyup(function (e) {
      if (e.key === "Escape") {
        $('#profileOverlay').removeClass('active');
      }
    });
  });
</script>

</body>
</html>
