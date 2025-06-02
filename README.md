<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Taquería MS</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Playfair+Display:wght@400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        :root {
            --primary: #d97706;
            --secondary: #f59e0b;
            --accent: #fbbf24;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #fff7ed;
            padding-top: 60px; /* Espacio para el navbar fijo */
        }
        
        h1, h2, h3 {
            font-family: 'Playfair Display', serif;
        }
        
        .card {
            perspective: 1000px;
            height: 380px;
        }
        
        .card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            transition: transform 0.8s;
            transform-style: preserve-3d;
        }
        
        .card:hover .card-inner {
            transform: rotateY(180deg);
        }
        
        .card-front, .card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }
        
        .card-back {
            background: white;
            transform: rotateY(180deg);
            display: flex;
            flex-direction: column;
            padding: 20px;
        }
        
        .card-img {
            height: 70%;
            width: 100%;
            object-fit: cover;
            transition: all 0.5s ease;
        }
        
        .card:hover .card-img {
            transform: scale(1.05);
        }
        
        .floating {
            animation: floating 3s ease-in-out infinite;
        }
        
        @keyframes floating {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }
        
        .btn-primary {
            background-color: var(--primary);
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            background-color: #b65c04;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(217, 119, 6, 0.4);
        }
        
        .section-title {
            position: relative;
            display: inline-block;
        }
        
        .section-title:after {
            content: '';
            position: absolute;
            width: 50%;
            height: 3px;
            background: var(--accent);
            bottom: -10px;
            left: 25%;
        }
        
        .chip {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        
        .chip.hot {
            background-color: #fef2f2;
            color: #dc2626;
        }
        
        .chip.veg {
            background-color: #ecfdf5;
            color: #059669;
        }
        
        .chip.new {
            background-color: #eff6ff;
            color: #2563eb;
        }

        /* Estilos para cards de Tacos/Burritos */
        .taco-burrito-card {
            animation: cardJump 3s ease infinite;
            background: linear-gradient(135deg, #fff7ed 0%, #ffedd5 100%);
            box-shadow: 0 10px 25px rgba(239, 68, 68, 0.3), 
                        0 0 0 3px rgba(239, 68, 68, 0.1),
                        0 0 20px 5px rgba(252, 211, 77, 0.3) inset;
            border-radius: 15px;
            overflow: hidden;
            transition: all 0.5s ease;
        }

        /* Estilos para cards de Bebidas */
        .bebida-card {
            animation: cardFloat 3s ease infinite;
            background: linear-gradient(135deg, #e0f2fe 0%, #bfdbfe 100%);
            box-shadow: 0 10px 25px rgba(30, 58, 138, 0.3), 
                        0 0 0 3px rgba(30, 58, 138, 0.1),
                        0 0 20px 5px rgba(147, 197, 253, 0.3) inset;
            border-radius: 15px;
            overflow: hidden;
            transition: all 0.5s ease;
        }

        @keyframes cardJump {
            0% { transform: translateY(0) scale(1); }
            50% { transform: translateY(-8px) scale(1.02); }
            100% { transform: translateY(0) scale(1); }
        }

        @keyframes cardFloat {
            0% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-8px) rotate(1deg); }
            100% { transform: translateY(0) rotate(0deg); }
        }

        /* Ajustes para móvil */
        @media (max-width: 767px) {
            #slider-container {
                scroll-snap-type: x mandatory;
                overflow-x: scroll;
                scroll-behavior: smooth;
            }
            #slider-container > div {
                scroll-snap-align: start;
            }
            /* Ocultar scrollbar */
            #slider-container::-webkit-scrollbar {
                display: none;
            }
        }
        
        /* Transición suave para el menú */
        #mobile-menu {
            transition: all 0.3s ease;
            max-height: 0;
            overflow: hidden;
        }
        #mobile-menu:not(.hidden) {
            max-height: 300px;
        }
    </style>
</head>
<body>
    <!-- Navbar Mobile Optimizado -->
    <nav class="fixed top-0 left-0 right-0 z-50 py-3 px-4 bg-white bg-opacity-90 backdrop-filter backdrop-blur-lg shadow-sm">
        <div class="flex justify-between items-center max-w-7xl mx-auto">
            <a href="#" class="text-xl md:text-2xl font-bold text-gray-800">
                <span class="text-amber-600">Taquería</span> MS
            </a>
            
            <!-- Menú Desktop (oculto en móvil) -->
            <div class="hidden md:flex space-x-6">
                <a href="#tacos" class="font-medium hover:text-amber-600 transition">Tacos/Burritos</a>
                <a href="#bebidas" class="font-medium hover:text-amber-600 transition">Bebidas</a>
                <a href="#contacto" class="font-medium hover:text-amber-600 transition">Contacto</a>
            </div>
            
            <!-- Botón Hamburguesa (solo móvil) -->
            <button id="menu-toggle" class="md:hidden text-gray-800 focus:outline-none">
                <i class="fas fa-bars text-xl"></i>
            </button>
        </div>
        
        <!-- Menú Desplegable Mobile -->
        <div id="mobile-menu" class="md:hidden hidden absolute top-full left-0 right-0 bg-white shadow-lg py-2 px-4">
            <a href="#tacos" class="block py-2 px-4 font-medium hover:text-amber-600 transition border-b border-gray-100">Tacos & Burritos</a>
            <a href="#bebidas" class="block py-2 px-4 font-medium hover:text-amber-600 transition border-b border-gray-100">Bebidas</a>
            <a href="#contacto" class="block py-2 px-4 font-medium hover:text-amber-600 transition">Contacto</a>
        </div>
    </nav>

    <!-- Hero Section Mobile-Friendly -->
<section class="relative h-80 md:h-screen max-h-[700px] overflow-hidden" id="hero-slider">
 <!-- Slider Container -->
<div class="relative w-full h-full flex" id="slider-container">

    <!-- Imagen 1 -->
    <div class="min-w-full h-full relative flex-shrink-0 transition-opacity duration-500 ease-in-out opacity-100">
        <div class="absolute inset-0 overflow-hidden">
            <img src="imagenes/taco_de_bistec.jpg" 
                 alt="Tacos de bistec" 
                 class="w-full h-full object-cover object-center" loading="lazy">
        </div>
        <div class="absolute inset-0 bg-black bg-opacity-40"></div>
    </div>

    <!-- Imagen 2 -->
    <div class="min-w-full h-full relative flex-shrink-0 transition-opacity duration-500 ease-in-out opacity-0">
        <div class="absolute inset-0 overflow-hidden">
            <img src="imagenes/Taco-de-alambre.jpg"
                 alt="Tacos de alambre" 
                 class="w-full h-full object-cover object-center" loading="lazy">
        </div>
        <div class="absolute inset-0 bg-black bg-opacity-40"></div>
    </div>

    <!-- Imagen 3 -->
    <div class="min-w-full h-full relative flex-shrink-0 transition-opacity duration-500 ease-in-out opacity-0">
        <div class="absolute inset-0 overflow-hidden">
            <img src="imagenes/burrito_de_longaniza.png"
                 alt="Burrito de longaniza" 
                 class="w-full h-full object-cover object-center" loading="lazy">
        </div>
        <div class="absolute inset-0 bg-black bg-opacity-40"></div>
    </div>

    <!-- Imagen 4 -->
    <div class="min-w-full h-full relative flex-shrink-0 transition-opacity duration-500 ease-in-out opacity-0">
        <div class="absolute inset-0 overflow-hidden">
            <img src="imagenes/burrito_de_enchilada.jpeg" 
                 alt="Burrito de enchilada" 
                 class="w-full h-full object-cover object-center" loading="lazy">
        </div>
        <div class="absolute inset-0 bg-black bg-opacity-40"></div>
    </div>

</div>


</div>

    </div>
    
    <!-- Contenido del Hero -->
    <div class="absolute inset-0 flex flex-col items-center justify-center text-center text-white z-10 px-6">
        <h1 class="text-3xl md:text-6xl font-bold mb-4">Auténticos Tacos Mexicanos</h1>
        <p class="text-lg md:text-2xl mb-6 max-w-3xl">Sabores tradicionales con un toque moderno</p>
        <a href="#tacos" class="inline-block bg-amber-500 hover:bg-amber-600 text-white font-bold py-2 px-6 md:py-3 md:px-8 rounded-full transition-all transform hover:scale-105 text-sm md:text-base">
            Ver Menú
        </a>
    </div>
    
    <!-- Indicadores -->
    <div class="absolute bottom-4 left-0 right-0 flex justify-center space-x-2 z-10">
        <button class="w-3 h-3 rounded-full bg-white bg-opacity-100 slider-dot" data-index="0"></button>
        <button class="w-3 h-3 rounded-full bg-white bg-opacity-60 slider-dot" data-index="1"></button>
        <button class="w-3 h-3 rounded-full bg-white bg-opacity-60 slider-dot" data-index="2"></button>
        <button class="w-3 h-3 rounded-full bg-white bg-opacity-60 slider-dot" data-index="3"></button>
    </div>
</section>

<script>
    // Slider mejorado
    document.addEventListener('DOMContentLoaded', function() {
        const sliderContainer = document.getElementById('slider-container');
        const slides = Array.from(document.querySelectorAll('#slider-container > div'));
        const dots = Array.from(document.querySelectorAll('.slider-dot'));
        let currentIndex = 0;
        let isAnimating = false;
        let autoSlideInterval;
        
        // Función para cambiar de slide
        function goToSlide(index) {
            if (isAnimating || index === currentIndex) return;
            
            isAnimating = true;
            
            // Actualizar estado de los slides
            slides[currentIndex].classList.remove('opacity-100');
            slides[currentIndex].classList.add('opacity-0');
            
            slides[index].classList.remove('opacity-0');
            slides[index].classList.add('opacity-100');
            
            // Actualizar dots
            dots[currentIndex].classList.remove('bg-opacity-100');
            dots[currentIndex].classList.add('bg-opacity-60');
            
            dots[index].classList.remove('bg-opacity-60');
            dots[index].classList.add('bg-opacity-100');
            
            currentIndex = index;
            
            // Resetear la animación
            setTimeout(() => {
                isAnimating = false;
            }, 500);
        }
        
        // Función para el siguiente slide
        function nextSlide() {
            const nextIndex = (currentIndex + 1) % slides.length;
            goToSlide(nextIndex);
        }
        
        // Iniciar slider automático
        function startAutoSlide() {
            autoSlideInterval = setInterval(nextSlide, 5000);
        }
        
        // Detener slider automático
        function stopAutoSlide() {
            clearInterval(autoSlideInterval);
        }
        
        // Eventos para los dots
        dots.forEach(dot => {
            dot.addEventListener('click', function() {
                const slideIndex = parseInt(this.dataset.index);
                if (slideIndex !== currentIndex) {
                    stopAutoSlide();
                    goToSlide(slideIndex);
                    startAutoSlide();
                }
            });
        });
        
        // Touch events para móviles
        let touchStartX = 0;
        let touchEndX = 0;
        
        sliderContainer.addEventListener('touchstart', e => {
            touchStartX = e.changedTouches[0].screenX;
            stopAutoSlide();
        }, { passive: true });
        
        sliderContainer.addEventListener('touchend', e => {
            touchEndX = e.changedTouches[0].screenX;
            handleSwipe();
            startAutoSlide();
        }, { passive: true });
        
        function handleSwipe() {
            const diff = touchStartX - touchEndX;
            const threshold = 50; // mínimo de desplazamiento para cambiar slide
            
            if (diff > threshold && currentIndex < slides.length - 1) {
                // Swipe izquierda - siguiente slide
                goToSlide(currentIndex + 1);
            } else if (diff < -threshold && currentIndex > 0) {
                // Swipe derecha - slide anterior
                goToSlide(currentIndex - 1);
            }
        }
        
        // Iniciar
        startAutoSlide();
        
        // Pausar auto slide cuando el mouse está sobre el slider
        sliderContainer.addEventListener('mouseenter', stopAutoSlide);
        sliderContainer.addEventListener('mouseleave', startAutoSlide);
    });
</script>

    <!-- Main Content -->
    <div class="max-w-7xl mx-auto px-6 md:px-12 py-12">
         <!-- Sección Tacos & Burritos -->
    <section id="tacos" class="max-w-7xl mx-auto px-6 md:px-12 py-12">
        <h2 class="section-title text-3xl md:text-4xl font-bold text-center mb-16">Tacos & Burritos</h2>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Taco 1 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/taco_de_bistec.jpg" 
                         alt="Taco de bistec" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3 flex space-x-2">
                        <span class="chip hot">	🔹 Clásico</span>
                        <span class="chip new">Popular</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Bistec</h3>
                        <span class="text-lg font-bold text-amber-600">$30</span>
                    </div>
                    <p class="text-gray-600 mt-2">Delicioso bistec de res a la plancha, bien sazonado y servido en tortilla de maíz</p>
                </div>
            </div>
            
            <!-- Taco 2 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Taco de longaniza.jpeg" 
                         alt="Taco de longaniza" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot"> 🌶️ Picante</span>
                        <span class="chip new">Popular</span>   
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Longaniza</h3>
                        <span class="text-lg font-bold text-amber-600">$30</span>
                    </div>
                    <p class="text-gray-600 mt-2">Longaniza roja con un toque picosito, perfecta para los amantes del sabor intenso.</p>
                </div>
            </div>
            
            <!-- Taco 3 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Taco campechano.jpeg" 
                         alt="Taco Campechano (bistec + longaniza)" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip veg">🔀 Mixto</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Taco Campechano (bistec + longaniza)</h3>
                        <span class="text-lg font-bold text-amber-600">$30</span>
                    </div>
                    <p class="text-gray-600 mt-2">La fusión ideal entre carne y embutido, llena de textura y sazón.</p>
                </div>
            </div>
            
            <!-- Taco 4 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Taco de chuleta.webp" 
                         alt="Taco de Chuleta" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3 flex space-x-2">
                        <span class="chip new">🔥 Ahumado</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Chuleta</h3>
                        <span class="text-lg font-bold text-amber-600">$30</span>
                    </div>
                    <p class="text-gray-600 mt-2">Carne de chuleta con un dorado crujiente por fuera y suave por dentro.</p>
                </div>
            </div>
            
            <!-- Taco 5 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Taco de enchilada.jpeg" 
                         alt="Taco de Enchilada" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot">🌶️ Picante</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Enchilada</h3>
                        <span class="text-lg font-bold text-amber-600">$30</span>
                    </div>
                    <p class="text-gray-600 mt-2">Carne de cerdo marinada en chile rojo y especias, cocinada hasta quedar suave y sabrosa.</p>
                </div>
            </div>
            <!-- Taco 6 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Taco hawuaiiano.jpg" 
                         alt="Tacos de Hawaiano" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot">🌴 Tropical</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Hawaiano</h3>
                        <span class="text-lg font-bold text-amber-600">$32</span>
                    </div>
                    <p class="text-gray-600 mt-2">Bistec acompañado de piña dorada. Dulce, salado y muy sabroso.</p>
                </div>
            </div>
            <!-- Taco 7 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Taco-de-alambre.jpg" 
                         alt="Tacos de alambre" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot">🧩 Completo/Mixto</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Alambre</h3>
                        <span class="text-lg font-bold text-amber-600">$32</span>
                    </div>
                    <p class="text-gray-600 mt-2"> Bistec con tocino, cebolla, pimientos y queso fundido. ¡Todo lo bueno en uno!</p>
                </div>
            </div>
            <!-- Burrito 1 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Burrito de bistec.jpeg" 
                         alt="Burrito de bistec" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot">	🔹 Clásico</span>
                        <span class="chip hot">	Popular</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Burrito de bistec</h3>
                        <span class="text-lg font-bold text-amber-600">$48</span>
                    </div>
                    <p class="text-gray-600 mt-2"> Bistec de res jugoso envuelto en tortilla de harina con queso.</p>
                </div>
            </div>
            <!-- Burrito 2 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/burrito_de_longaniza.png" 
                         alt="Burrito de longaniza" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot">🌶️ Picante</span>
                        <span class="chip hot">	Popular</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Burrito de longaniza</h3>
                        <span class="text-lg font-bold text-amber-600">$48</span>
                    </div>
                    <p class="text-gray-600 mt-2">Longaniza bien dorada y picosita, queso y verduritas.</p>
                </div>
            </div>
            <!-- Burrito 3-->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/burritos campechanos.png" 
                         alt="Burrito Campechano" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot">🔀 Mixto</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Burrito Campechano</h3>
                        <span class="text-lg font-bold text-amber-600">$48</span>
                    </div>
                    <p class="text-gray-600 mt-2"> Mezcla irresistible de bistec y longaniza en tortilla de harina, con queso.</p>
                </div>
            </div>
        <!-- Burrito 4 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Burrito de chuleta.jpeg" 
                         alt="Burrito de chuleta" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">t
                        <span class="chip hot">	🔥 Ahumado</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Burrito de Chuleta</h3>
                        <span class="text-lg font-bold text-amber-600">$48</span>
                    </div>
                    <p class="text-gray-600 mt-2">Chuleta de cerdo a la plancha, con sabor ahumado, acompañada de queso y salsa.</p>
                </div>
            </div>
            <!-- Burrito 5 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/burrito_de_enchilada.jpeg" 
                         alt="Burrito de Enchilada" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip hot">🌶️ Picante</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Burrito de Enchilada</h3>
                        <span class="text-lg font-bold text-amber-600">$48</span>
                    </div>
                    <p class="text-gray-600 mt-2">Carne adobada al estilo enchilado y queso fundido.</p>
                </div>
            </div>
        <!-- Burrito 6 -->
        <div class="taco-burrito-card">
            <div class="relative h-48 overflow-hidden">
                <img src="imagenes/Burrito de alambre.png" 
                     alt="Burrito de Alambre" 
                     class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                <div class="absolute top-3 right-3">
                    <span class="chip hot">	🧩 Completo/Mixto</span>
                </div>
            </div>
            <div class="p-5">
                <div class="flex justify-between items-center">
                    <h3 class="text-xl font-bold text-gray-800">Burrito de Alambre</h3>
                    <span class="text-lg font-bold text-amber-600">$47</span>
                </div>
                <p class="text-gray-600 mt-2">Bistec, tocino, cebolla, pimientos y queso fundido en tortilla gigante. ¡Una bomba!</p>
            </div>
        </div>
            <!-- Burrito 7 -->
            <div class="taco-burrito-card">
                <div class="relative h-48 overflow-hidden">
                    <img src="imagenes/Burrito Supremo.jpeg" 
                         alt="Burrito Supremo" 
                         class="w-full h-full object-cover transition-transform duration-500 hover:scale-105">
                    <div class="absolute top-3 right-3">
                        <span class="chip veg">	⭐ Especialidad</span>
                    </div>
                </div>
                <div class="p-5">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold text-gray-800">Burrito Supremo</h3>
                        <span class="text-lg font-bold text-amber-600">$75</span>
                    </div>
                    <p class="text-gray-600 mt-2"> Burrito supremo con bistec, longaniza, chuleta, carne enchilada, pechuga de pollo, alambre y queso Oaxaca. ¡El rey de los burritos!</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Sección Bebidas -->
    <section id="bebidas" class="max-w-7xl mx-auto px-6 md:px-12 py-12">
        <h2 class="section-title text-3xl md:text-4xl font-bold text-center mb-16">Bebidas</h2>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Bebida 1 -->
            <div class="bebida-card">
    <div class="relative h-48 overflow-hidden bg-white flex items-center justify-center">
        <img src="imagenes/7up.webp" 
             alt="Refresco 7up" 
             class="w-full h-full object-contain transition-transform duration-500 hover:scale-90">
    </div>
    <div class="p-5">
        <div class="flex justify-between items-center">
            <h3 class="text-xl font-bold text-gray-800">🟢 7UP</h3>
            <span class="text-lg font-bold text-blue-600">$25</span>
        </div>
        <p class="text-gray-600 mt-2">Refresco de limón-lima sin cafeína. Refrescante y burbujeante, ideal para acompañar tacos.</p>
    </div>
</div>

            <!-- Bebida 2 -->
<div class="bebida-card">
    <div class="relative h-48 overflow-hidden bg-white flex items-center justify-center">
        <img src="imagenes/Manzanita.jpeg" 
             alt="Refresco de Manzana" 
             class="w-full h-full object-contain transition-transform duration-500 hover:scale-105">
    </div>
    <div class="p-5">
        <div class="flex justify-between items-center">
            <h3 class="text-xl font-bold text-gray-800">🍎 Manzanita</h3>
            <span class="text-lg font-bold text-blue-600">$25</span>
        </div>
        <p class="text-gray-600 mt-2">Refresco de manzana con sabor dulce y ligero. Ideal para niños y adultos.</p>
    </div>
</div>

<!-- Bebida 3 -->
<div class="bebida-card">
    <div class="relative h-48 overflow-hidden bg-white flex items-center justify-center">
        <img src="imagenes/Sangria.png" 
             alt="Refresco de Sangria" 
             class="w-full h-full object-contain transition-transform duration-500 hover:scale-105">
    </div>
    <div class="p-5">
        <div class="flex justify-between items-center">
            <h3 class="text-xl font-bold text-gray-800">🍷 Sangría Señorial</h3>
            <span class="text-lg font-bold text-blue-600">$25</span>
        </div>
        <p class="text-gray-600 mt-2">Refresco con sabor a uva y toques especiados. Sabe a fiesta en cada trago.</p>
    </div>
</div>

<!-- Bebida 4 -->
<div class="bebida-card">
    <div class="relative h-48 overflow-hidden bg-white flex items-center justify-center">
        <img src="imagenes/Mirinda.jpeg" 
             alt="Refresco Mirinda" 
             class="w-full h-full object-contain transition-transform duration-500 hover:scale-105">
    </div>
    <div class="p-5">
        <div class="flex justify-between items-center">
            <h3 class="text-xl font-bold text-gray-800">🍊 Mirinda</h3>
            <span class="text-lg font-bold text-blue-600">$25</span>
        </div>
        <p class="text-gray-600 mt-2">Sabor a naranja intenso y dulce. Muy popular entre los amantes del sabor afrutado.</p>
    </div>
</div>

<!-- Bebida 5 -->
<div class="bebida-card">
    <div class="relative h-48 overflow-hidden bg-white flex items-center justify-center">
        <img src="imagenes/Squirt.jpeg" 
             alt="Refresco Squirt" 
             class="w-full h-full object-contain transition-transform duration-500 hover:scale-105">
    </div>
    <div class="p-5">
        <div class="flex justify-between items-center">
            <h3 class="text-xl font-bold text-gray-800">🟡 Squirt</h3>
            <span class="text-lg font-bold text-blue-600">$25</span>
        </div>
        <p class="text-gray-600 mt-2">Refresco de toronja con un toque ácido y burbujeante. Perfecto para los que buscan algo diferente.</p>
    </div>
</div>

<!-- Bebida 6 -->
<div class="bebida-card">
    <div class="relative h-48 overflow-hidden bg-white flex items-center justify-center">
        <img src="imagenes/Pepsi.jpeg" 
             alt="Refresco Pepsi" 
             class="w-full h-full object-contain transition-transform duration-500 hover:scale-105">
    </div>
    <div class="p-5">
        <div class="flex justify-between items-center">
            <h3 class="text-xl font-bold text-gray-800">🔵 Pepsi</h3>
            <span class="text-lg font-bold text-blue-600">$25</span>
        </div>
        <p class="text-gray-600 mt-2">Refresco de cola con sabor dulce y chispeante. Un clásico que nunca falla.</p>
    </div>
</div>

    </section>
    </div>

    <!-- Contact Section -->
    <section id="contacto" class="bg-amber-50 py-16 px-6 md:px-12">
        <div class="max-w-4xl mx-auto text-center">
            <h2 class="text-3xl md:text-4xl font-bold mb-6">¿Listo para probar nuestros tacos?</h2>
            <p class="text-xl mb-8">Visítanos o pide a domicilio</p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
                <div>
                    <i class="fas fa-map-marker-alt text-3xl text-amber-600 mb-4"></i>
                    <h3 class="font-bold mb-2">Dirección</h3>
                    <p>Av. Pantitlán 397, Evolución <br>57700 Cdad. Nezahualcóyotl, Méx.</p>
                </div>
                <div>
                    <i class="fas fa-clock text-3xl text-amber-600 mb-4"></i>
                    <h3 class="font-bold mb-2">Horario</h3>
                    <p>Lunes a Sábado 10:30 PM - 10:00 PM</p>
                    <p>Domingo 11:00 PM - 7:00 PM</p>
                </div>
            </div>
            
            <h3 class="font-bold mb-2">Redes sociales</h3><br>
            <div class="flex justify-center space-x-4">
                <!-- Redes sociales originales -->
                <a href="https://www.facebook.com/profile.php?id=100057819962963" title="Facebook" class="bg-amber-600 text-white w-12 h-12 rounded-full flex items-center justify-center text-xl hover:bg-amber-700 transition">
                    <i class="fab fa-facebook-f"></i>
                </a>
                <a href="https://www.instagram.com/tacosmsoficial/" title="Instagram" class="bg-amber-600 text-white w-12 h-12 rounded-full flex items-center justify-center text-xl hover:bg-amber-700 transition">
                    <i class="fab fa-instagram"></i>
                </a>
                <a href="#" title="WhatsApp" class="bg-amber-600 text-white w-12 h-12 rounded-full flex items-center justify-center text-xl hover:bg-amber-700 transition">
                    <i class="fab fa-whatsapp"></i>
                </a>
            </div><br><br>
            <h3 class="font-bold mb-2">Servicios de delivery</h3><br>
            <div class="flex justify-center space-x-4">
                <!-- Servicios de delivery -->
                <a href="https://www.ubereats.com/mx/store/tacos-ms/-Vq13bO8Qd6q7NKu22CYWA?diningMode=DELIVERY" title="Uber Eats" class="bg-black text-white w-12 h-12 rounded-full flex items-center justify-center text-xl hover:bg-gray-800 transition group relative">
                    <i class="fas fa-utensils"></i>
                    <span class="absolute -bottom-8 bg-black text-white text-xs px-2 py-1 rounded opacity-0 group-hover:opacity-100 transition-opacity">Uber Eats</span>
                </a>
                <a href="https://www.rappi.com.mx/restaurantes/1923778923-tacos-ms-pantitlan" title="Rappi" class="bg-green-600 text-white w-12 h-12 rounded-full flex items-center justify-center text-xl hover:bg-green-700 transition group relative">
                    <i class="fas fa-motorcycle"></i>
                    <span class="absolute -bottom-8 bg-green-600 text-white text-xs px-2 py-1 rounded opacity-0 group-hover:opacity-100 transition-opacity">Rappi</span>
                </a>
                <a href="#" title="Didi Food" class="bg-yellow-500 text-white w-12 h-12 rounded-full flex items-center justify-center text-xl hover:bg-yellow-600 transition group relative">
                    <i class="fas fa-car"></i>
                    <span class="absolute -bottom-8 bg-yellow-500 text-white text-xs px-2 py-1 rounded opacity-0 group-hover:opacity-100 transition-opacity">Didi Food</span>
                </a>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-12 px-6 md:px-12">
        <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8">
            <div>
                <h3 class="text-xl font-bold mb-4 text-amber-400">Taquería MS</h3>
                <p class="text-gray-400">Auténtica cocina mexicana desde 2010.</p>
            </div>
            <div>
                <h4 class="font-bold mb-4">Menú</h4>
                <ul class="space-y-2">
                    <li><a href="#tacos" class="text-gray-400 hover:text-amber-400 transition">Tacos/Burritos</a></li>
                    <li><a href="#bebidas" class="text-gray-400 hover:text-amber-400 transition">Bebidas</a></li>
                </ul>
            </div>
            <div>
                <h4 class="font-bold mb-4">Síguenos</h4>
                <div class="flex space-x-4">
                    <a href="#" class="text-gray-400 hover:text-amber-400 transition text-xl"><i class="fab fa-facebook-f"></i></a>
                    <a href="#" class="text-gray-400 hover:text-amber-400 transition text-xl"><i class="fab fa-instagram"></i></a>
                    <a href="#" class="text-gray-400 hover:text-amber-400 transition text-xl"><i class="fab fa-tiktok"></i></a>
                </div>
            </div>
        </div>
        <div class="border-t border-gray-800 mt-8 pt-8 text-center text-gray-400">
            <p>&copy; 2024 Taquería MS. Todos los derechos reservados.</p>
        </div>
    </footer>

    <!-- WhatsApp Button -->
    <a href="https://wa.me/525512345678?text=Hola,%20quisiera%20hacer%20un%20pedido" 
       class="fixed bottom-8 right-8 bg-green-500 text-white w-14 h-14 rounded-full flex items-center justify-center text-2xl shadow-lg floating">
        <i class="fab fa-whatsapp"></i>
    </a>

    <script>
        // Slider con Touch para Móviles
        document.addEventListener('DOMContentLoaded', function() {
            const slider = document.getElementById('slider-container');
            const slides = document.querySelectorAll('#slider-container > div');
            const dots = document.querySelectorAll('.slider-dot');
            let currentIndex = 0;
            let startX, moveX;
            const threshold = 50;
            
            // Touch Start
            slider.addEventListener('touchstart', (e) => {
                startX = e.touches[0].clientX;
                clearInterval(autoSlide);
            }, { passive: true });
            
            // Touch Move
            slider.addEventListener('touchmove', (e) => {
                if(!startX) return;
                moveX = e.touches[0].clientX;
                const diff = moveX - startX;
                slider.style.transform = `translateX(calc(-${currentIndex * 100}% + ${diff}px))`;
            }, { passive: true });
            
            // Touch End
            slider.addEventListener('touchend', (e) => {
                if(!startX) return;
                const diff = moveX - startX;
                
                if(diff > threshold && currentIndex > 0) {
                    // Swipe Right
                    showSlide(currentIndex - 1);
                } else if(diff < -threshold && currentIndex < slides.length - 1) {
                    // Swipe Left
                    showSlide(currentIndex + 1);
                } else {
                    // Vuelve a la posición actual
                    slider.style.transform = `translateX(-${currentIndex * 100}%)`;
                }
                
                startX = null;
                moveX = null;
                startAutoSlide();
            });
            
            // Función para mostrar slide
            function showSlide(index) {
                currentIndex = index;
                slider.style.transform = `translateX(-${currentIndex * 100}%)`;
                
                // Actualizar dots
                dots.forEach(dot => {
                    dot.classList.toggle('active', parseInt(dot.dataset.index) === index);
                    dot.classList.toggle('bg-opacity-60', parseInt(dot.dataset.index) !== index);
                    dot.classList.toggle('bg-opacity-100', parseInt(dot.dataset.index) === index);
                });
            }
            
            // Navegación por dots
            dots.forEach(dot => {
                dot.addEventListener('click', function() {
                    showSlide(parseInt(this.dataset.index));
                });
            });
            
            // Slider automático
            let autoSlide;
            function startAutoSlide() {
                autoSlide = setInterval(() => {
                    const nextIndex = (currentIndex + 1) % slides.length;
                    showSlide(nextIndex);
                }, 6000);
            }
            startAutoSlide();
            
            // Menú Hamburguesa
            const menuToggle = document.getElementById('menu-toggle');
            const mobileMenu = document.getElementById('mobile-menu');
            
            menuToggle.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
                menuToggle.innerHTML = mobileMenu.classList.contains('hidden') ? 
                    '<i class="fas fa-bars text-xl"></i>' : 
                    '<i class="fas fa-times text-xl"></i>';
            });

            // Cerrar menú al hacer clic en un enlace (solo móvil)
            document.querySelectorAll('#mobile-menu a').forEach(link => {
                link.addEventListener('click', () => {
                    mobileMenu.classList.add('hidden');
                    menuToggle.innerHTML = '<i class="fas fa-bars text-xl"></i>';
                });
            });
        });
    </script>
</body>
</html> 
