
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AURA Unisex Salon</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@700&family=Montserrat:wght@100;200;400;600&display=swap" rel="stylesheet">
<style>
:root{
  --gold:#D4AF37;
  --glass: rgba(0,0,0,0.7);
  --border: rgba(212,175,55,0.25);
  --transition: all 0.4s ease;
}
*{margin:0;padding:0;box-sizing:border-box;font-family:'Montserrat',sans-serif;}
body{background:linear-gradient(45deg,#1a1a2e 0%,#16213e 50%,#0f3460 100%);color:#fff;overflow-x:hidden;scroll-behavior:smooth;}

/* FIXED Background Videos */
#bg-container{position:fixed;inset:0;z-index:-2;overflow:hidden;}
#mainVideo, #overlayVideo{position:absolute;top:0;left:0;width:100%;height:100%;object-fit:cover;}
#mainVideo{background:#1a1a2e;} /* Solid fallback */
#overlayVideo{opacity:0.35;}

/* FAST Intro - 1.5s instead of 3s */
#intro{position:fixed;inset:0;display:flex;justify-content:center;align-items:center;background:#000;z-index:10000;transition:opacity 0.8s;}
#intro.hidden{opacity:0;pointer-events:none;}
#intro img{width:200px;animation:logoReveal 1s forwards;}
@keyframes logoReveal{0%{opacity:0;transform:scale(0.5);}100%{opacity:1;transform:scale(1);}}

/* Navigation */
nav{
  position:fixed;top:0;width:100%;padding:15px 5%;
  display:flex;justify-content:space-between;align-items:center;z-index:1000;
  backdrop-filter:blur(20px);border-bottom:1px solid var(--border);
  background:rgba(0,0,0,0.4);
}
.nav-logo{font-family:'Cinzel Decorative';color:var(--gold);font-size:22px;letter-spacing:4px;cursor:pointer;}
nav .nav-links{display:flex;gap:15px;}
nav .nav-links div{cursor:pointer;color:#fff;font-weight:500;transition:var(--transition);padding:8px 12px;}
nav .nav-links div:hover{color:var(--gold);}

/* Sections */
section{min-height:100vh;padding:110px 5% 60px;opacity:0;transform:translateY(30px);transition:var(--transition);}
section.visible{opacity:1;transform:translateY(0);}

/* Glass Cards */
.glassCard{background:var(--glass);backdrop-filter:blur(20px);border:1px solid var(--border);border-radius:15px;padding:25px;margin:15px 0;}

/* Hero Title */
.hero-title{font-family:'Cinzel Decorative';font-size:clamp(2.5rem,8vw,6rem);color:var(--gold);letter-spacing:8px;text-align:center;margin:30px 0;animation:breathe 6s infinite alternate;}
@keyframes breathe{0%,100%{letter-spacing:8px;}50%{letter-spacing:12px;}}

/* Counters */
.counters{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:20px;margin-top:30px;}
.counters div{text-align:center;padding:20px;background:var(--glass);border-radius:12px;border:1px solid var(--border);}
.counters h3{font-size:2rem;color:var(--gold);margin-bottom:5px;}

/* ULTRA RESPONSIVE Service Cards */
.serviceCards{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:25px;padding:30px 10px;max-width:1400px;margin:0 auto;}
.serviceCard{position:relative;overflow:hidden;border-radius:20px;box-shadow:0 10px 40px rgba(0,0,0,0.3);transition:var(--transition);cursor:pointer;}
.serviceCard:hover{transform:translateY(-20px) scale(1.03);box-shadow:0 20px 60px rgba(212,175,55,0.3);}
.serviceCard img{width:100%;height:250px;object-fit:cover;display:block;transition:var(--transition);}
.serviceCard .overlay{position:absolute;inset:0;background:linear-gradient(transparent 60%,rgba(0,0,0,0.9));opacity:0;transition:var(--transition);}
.serviceCard:hover .overlay{opacity:1;}
.serviceCard .content{position:absolute;bottom:25px;left:25px;right:25px;color:#fff;transform:translateY(30px);transition:var(--transition);}
.serviceCard:hover .content{transform:translateY(0);}
.serviceCard h3{font-family:'Cinzel Decorative';font-size:1.8rem;margin-bottom:8px;text-shadow:0 2px 10px rgba(0,0,0,0.8);}
.serviceCard p{font-size:1rem;opacity:0.9;}

/* Service Selector */
.service-selector{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px;max-width:900px;margin:25px auto;padding:0 15px;}
.service-checkbox{position:relative;}
.service-checkbox input[type="checkbox"]{display:none;}
.service-checkbox label{display:block;padding:20px;border:2px solid var(--border);border-radius:12px;text-align:center;cursor:pointer;transition:var(--transition);background:var(--glass);font-weight:500;}
.service-checkbox input:checked + label{background:linear-gradient(45deg,var(--gold),#ffed4a);color:#000;border-color:var(--gold);transform:translateY(-5px) scale(1.02);box-shadow:0 10px 30px rgba(212,175,55,0.4);}
.service-checkbox input:checked + label::after{content:'✓';position:absolute;top:12px;right:12px;font-size:22px;font-weight:bold;color:#000;}
.selected-services{display:flex;flex-wrap:wrap;gap:12px;margin-top:20px;padding:20px;background:linear-gradient(45deg,rgba(212,175,55,0.1),rgba(212,175,55,0.05));border:1px solid var(--border);border-radius:15px;min-height:50px;}
.selected-services span{background:linear-gradient(45deg,var(--gold),#ffed4a);color:#000;padding:10px 18px;border-radius:25px;font-weight:700;font-size:14px;animation:popIn 0.4s ease;}

/* Gallery */
.gallery-container{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;padding:40px 10px;max-width:1400px;margin:0 auto;}
.gallery-container img{width:100%;height:220px;object-fit:cover;border-radius:15px;transition:var(--transition);cursor:pointer;border:3px solid transparent;}
.gallery-container img:hover{transform:scale(1.05);border-color:var(--gold);}

/* Booking Form */
#bookingForm{display:grid;gap:20px;max-width:700px;margin:40px auto;padding:40px;}
#bookingForm input,#bookingForm select{padding:18px;border-radius:12px;border:1px solid var(--border);outline:none;background:var(--glass);color:#fff;font-size:16px;}
#bookingForm button{background:linear-gradient(45deg,var(--gold),#ffed4a);color:#000;font-weight:800;cursor:pointer;transition:var(--transition);font-size:18px;border:none;padding:20px;}
#bookingForm button:hover{transform:scale(1.08) translateY(-3px);box-shadow:0 15px 40px rgba(212,175,55,0.4);}

/* Lightbox & Thank You */
#lightbox{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.95);justify-content:center;align-items:center;z-index:20000;flex-direction:column;}
#lightbox img{max-width:90%;max-height:90%;border-radius:15px;}
#lightbox .close{position:absolute;top:30px;right:30px;font-size:45px;cursor:pointer;color:var(--gold);}
#thankYou{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.92);justify-content:center;align-items:center;z-index:30000;}
#thankYou .glassCard{padding:50px;text-align:center;max-width:600px;}
.confetti{position:absolute;width:14px;height:14px;border-radius:50%;animation:fall 3s linear infinite;}
@keyframes fall{0%{transform:translateY(-60px);}100%{transform:translateY(100vh);}}
@keyframes popIn{0%{transform:scale(0) rotate(-180deg);opacity:0;}100%{transform:scale(1) rotate(0);opacity:1;}}

/* RESPONSIVE */
@media(max-width:1000px){
  .serviceCards{grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;}
}
@media(max-width:768px){
  nav{padding:12px 20px;}
  nav .nav-links{position:fixed;top:100%;left:0;width:100%;background:rgba(0,0,0,0.98);flex-direction:column;padding:20px;display:none;}
  nav .nav-links.active{display:flex;gap:0;}
  .serviceCards{grid-template-columns:1fr;gap:20px;}
  .service-selector{grid-template-columns:repeat(2,1fr);}
  section{padding:90px 15px 50px;}
}
@media(max-width:480px){
  .service-selector{grid-template-columns:1fr;}
  .gallery-container{grid-template-columns:repeat(2,1fr);}
  #bookingForm{padding:25px;}
}
</style>
</head>
<body>

<!-- FAST Intro (1.5s) -->
<div id="intro">
  <img src="https://via.placeholder.com/200x200/D4AF37/000?text=AURA" alt="AURA Logo">
</div>

<!-- FIXED Background Videos -->
<div id="bg-container">
  <video id="mainVideo" autoplay muted loop playsinline preload="metadata" poster="https://images.unsplash.com/photo-1511699656952-34342bb7c2f2?ixlib=rb-4.0.3&w=1920&q=80">
    <source src="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4" type="video/mp4">
  </video>
  <video id="overlayVideo" autoplay muted loop playsinline preload="metadata" style="opacity:0.35;">
    <source src="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4" type="video/mp4">
  </video>
</div>

<!-- Navigation -->
<nav>
  <div class="nav-logo" onclick="scrollToSection('home')">AURA</div>
  <div class="nav-links" id="navLinks">
    <div onclick="scrollToSection('home');closeMobileNav()">Home</div>
    <div onclick="scrollToSection('about');closeMobileNav()">About</div>
    <div onclick="scrollToSection('services');closeMobileNav()">Services</div>
    <div onclick="scrollToSection('gallery');closeMobileNav()">Gallery</div>
    <div onclick="scrollToSection('booking');closeMobileNav()">Booking</div>
  </div>
</nav>

<!-- Sections -->
<section id="home" class="visible">
  <div style="text-align:center;">
    <h1 class="hero-title">AURA Unisex Salon</h1>
    <p style="font-size:1.5rem;margin-top:25px;opacity:0.9;">Premium Hair & Beauty Services</p>
  </div>
</section>

<section id="about">
  <div class="glassCard" style="max-width:1100px;margin:0 auto;">
    <h2 style="color:var(--gold);font-family:'Cinzel Decorative';font-size:2.5rem;margin-bottom:25px;">About AURA</h2>
    <p style="font-size:1.15rem;line-height:1.8;margin-bottom:35px;">Premium unisex salon offering world-class haircare, grooming, spa treatments, and beauty services with 15+ years of excellence.</p>
    <div class="counters">
      <div><h3>15+</h3><p>Years Exp.</p></div>
      <div><h3>5000+</h3><p>Happy Clients</p></div>
      <div><h3>4.9⭐</h3><p>Ratings</p></div>
    </div>
  </div>
</section>

<!-- ULTRA RESPONSIVE Services -->
<section id="services">
  <h2 style="color:var(--gold);text-align:center;font-family:'Cinzel Decorative';font-size:2.8rem;margin:40px 0 50px;">Our Premium Services</h2>
  <div class="serviceCards">
    <div class="serviceCard">
      <img src="https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?w=500&h=250&fit=crop" alt="Male Grooming">
      <div class="overlay"></div>
      <div class="content">
        <h3>Male Grooming</h3>
        <p>Advanced haircuts, beard styling, facials, shaves & premium grooming</p>
      </div>
    </div>
    <div class="serviceCard">
      <img src="https://images.unsplash.com/photo-1625772278107-9e826e69bcad?w=500&h=250&fit=crop" alt="Female Beauty">
      <div class="overlay"></div>
      <div class="content">
        <h3>Female Beauty</h3>
        <p>Hair styling, spa treatments, makeup, threading & bridal packages</p>
      </div>
    </div>
    <div class="serviceCard">
      <img src="https://images.unsplash.com/photo-1587300003388-59208b3e0d83?w=500&h=250&fit=crop" alt="Relaxation">
      <div class="overlay"></div>
      <div class="content">
        <h3>Relaxation Spa</h3>
        <p>Body massage, aromatherapy, head spa & therapeutic treatments</p>
      </div>
    </div>
  </div>
</section>

<section id="gallery">
  <h2 style="color:var(--gold);text-align:center;font-family:'Cinzel Decorative';font-size:2.8rem;margin-bottom:50px;">Gallery</h2>
  <div class="gallery-container">
    <img src="https://images.unsplash.com/photo-1574169208507-84376144848b?w=400&h=220&fit=crop" alt="Style 1">
    <img src="https://images.unsplash.com/photo-1603331842546-8e84dd946a43?w=400&h=220&fit=crop" alt="Style 2">
    <img src="https://images.unsplash.com/photo-1588880331178-7fdf2bd973f3?w=400&h=220&fit=crop" alt="Style 3">
    <img src="https://images.unsplash.com/photo-1581578731548-81b1e2f38d64?w=400&h=220&fit=crop" alt="Style 4">
    <img src="https://images.unsplash.com/photo-1611494423816-e645fc41c96f?w=400&h=220&fit=crop" alt="Style 5">
    <img src="https://images.unsplash.com/photo-1590846928537-69f98cfd9454?w=400&h=220&fit=crop" alt="Style 6">
  </div>
</section>

<!-- Booking -->
<section id="booking">
  <h2 style="color:var(--gold);text-align:center;font-family:'Cinzel Decorative';font-size:2.8rem;margin-bottom:40px;">Book Appointment</h2>
  <div style="max-width:800px;margin:auto;">
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:35px;">
      <button onclick="setBookingMode('single')" class="glassCard" style="padding:18px;font-weight:700;font-size:16px;border:none;cursor:pointer;">👤 Single</button>
      <button onclick="setBookingMode('family')" class="glassCard" style="padding:18px;font-weight:700;font-size:16px;border:none;cursor:pointer;">👨‍👩‍👧‍👦 Family</button>
    </div>
    <form id="bookingForm" class="glassCard">
      <div id="membersContainer"></div>
      <input type="tel" id="contact" placeholder="📞 Contact Number *" required>
      <input type="tel" id="whatsapp" placeholder="📱 WhatsApp *" required>
      <input type="email" id="email" placeholder="✉️ Email *" required>
      
      <div>
        <label style="display:block;font-weight:700;font-size:18px;color:var(--gold);margin-bottom:15px;">Services Required</label>
        <div class="service-selector">
          <div class="service-checkbox"><input type="checkbox" id="haircut" value="Haircut"><label for="haircut">✂️ Haircut</label></div>
          <div class="service-checkbox"><input type="checkbox" id="styling" value="Styling"><label for="styling">💇 Styling</label></div>
          <div class="service-checkbox"><input type="checkbox" id="facial" value="Facial"><label for="facial">✨ Facial</label></div>
          <div class="service-checkbox"><input type="checkbox" id="massage" value="Massage"><label for="massage">💆 Massage</label></div>
          <div class="service-checkbox"><input type="checkbox" id="beard" value="Beard"><label for="beard">🪒 Beard</label></div>
          <div class="service-checkbox"><input type="checkbox" id="spa" value="Spa"><label for="spa">🛁 Spa</label></div>
        </div>
        <div id="selectedServices" class="selected-services"></div>
      </div>
      
      <input type="date" id="date" required>
      <input type="time" id="time" required>
      <button type="submit">🚀 Confirm Booking</button>
    </form>
  </div>
</section>

<!-- Lightbox & Thank You -->
<div id="lightbox">
  <span class="close" onclick="closeLightbox()">&times;</span>
  <img id="lightboxImg" src="" alt=""/>
</div>
<div id="thankYou">
  <div class="glassCard">
    <h2 style="color:var(--gold);">✅ Booking Confirmed!</h2>
    <p id="bookingSummary" style="font-size:1.3rem;margin:20px 0;">Your services are booked!</p>
    <p>We'll call/WhatsApp you within 30 minutes to confirm.</p>
  </div>
</div>

<script>
// FIXED VIDEO + FAST INTRO + RESPONSIVE CARDS
document.addEventListener('DOMContentLoaded',()=>{
  // FAST intro (1.5s)
  setTimeout(()=>{
    document.getElementById('intro').classList.add('hidden');
    document.getElementById('home').classList.add('visible');
  }, 1500);
  
  // FIXED video autoplay
  const mainVideo = document.getElementById('mainVideo');
  const overlayVideo = document.getElementById('overlayVideo');
  
  function playVideos(){
    mainVideo.play().then(()=>console.log('✅ Main video playing')).catch(e=>console.log('Video blocked'));
    overlayVideo.play().catch(e=>console.log('Overlay blocked'));
  }
  
  // Try immediately + user interaction
  playVideos();
  ['click','scroll','touchstart','keydown'].forEach(evt=>{
    document.addEventListener(evt, playVideos, {once:true});
  });
});

// Smooth scroll + mobile nav
function scrollToSection(id){
  document.getElementById(id).scrollIntoView({behavior:'smooth'});
  document.getElementById(id).classList.add('visible');
  closeMobileNav();
}
function closeMobileNav(){document.getElementById('navLinks').classList.remove('active');}
function toggleMobileNav(){document.getElementById('navLinks').classList.toggle('active');}

// Service selection
function updateSelectedServices(){
  const checkboxes = document.querySelectorAll('.service-checkbox input:checked');
  const selectedDiv = document.getElementById('selectedServices');
  const summary = [];
  
  checkboxes.forEach(cb=>summary.push(cb.value));
  
  if(summary.length){
    selectedDiv.innerHTML = summary.map(s=>`<span>${s}</span>`).join('');
    selectedDiv.style.display = 'flex';
  } else {
    selectedDiv.style.display = 'none';
  }
  return summary;
}
document.querySelectorAll('.service-checkbox input').forEach(cb=>cb.addEventListener('change',updateSelectedServices));

// Booking
let bookingMode = 'single';
function setBookingMode(mode){
  bookingMode = mode;
  const container = document.getElementById('membersContainer');
  container.innerHTML = mode === 'single' 
    ? '<input type="text" placeholder="👤 Full Name *" required style="margin-bottom:18px;">'
    : '<input type="text" placeholder="👤 Member 1 *" required style="margin-bottom:12px;"><input type="text" placeholder="👤 Member 2 *" required style="margin-bottom:12px;"><input type="text" placeholder="👤 Member 3 *" required style="margin-bottom:12px;">';
}

// Booking submit
document.getElementById('bookingForm').addEventListener('submit',e=>{
  e.preventDefault();
  const services = updateSelectedServices();
  if(!services.length){
    alert('⚠️ Please select at least one service');
    return;
  }
  
  document.getElementById('bookingSummary').textContent = `${bookingMode === 'single' ? 'Single' : 'Family'} booking: ${services.join(', ')}`;
  document.getElementById('thankYou').style.display = 'flex';
  
  // Confetti explosion
  for(let i=0;i<80;i++){
    const confetti = document.createElement('div');
    confetti.className = 'confetti';
    confetti.style.cssText = `
      left:${Math.random()*100}vw;
      animation-delay:${Math.random()*0.5}s;
      background:${['#D4AF37','#ff6b6b','#4ecdc4','gold','white'][Math.floor(Math.random()*5)]};
    `;
    document.body.appendChild(confetti);
    setTimeout(()=>confetti.remove(),4500);
  }
  
  e.target.reset();
  setBookingMode('single');
  updateSelectedServices();
  setTimeout(()=>document.getElementById('thankYou').style.display='none',5000);
});

// Scroll animations
const observer = new IntersectionObserver(entries=>entries.forEach(entry=>entry.isIntersecting && entry.target.classList.add('visible')));
document.querySelectorAll('section:not(#home)').forEach(s=>observer.observe(s));
</script>
</body>
</html>
