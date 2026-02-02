<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>InfiniteSearch</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
/* ---------- GLOBAL ---------- */
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family: Arial, sans-serif;
}
body{
  min-height:100vh;
  background:linear-gradient(135deg,#0f2027,#203a43,#2c5364);
  color:white;
}

/* ---------- LOGIN PAGE ---------- */
#loginPage{
  display:flex;
  align-items:center;
  justify-content:center;
  height:100vh;
}
.login-card{
  width:320px;
  padding:25px;
  background:rgba(255,255,255,0.12);
  backdrop-filter:blur(12px);
  border-radius:14px;
  text-align:center;
}
.login-card h2{
  margin-bottom:20px;
}
.login-card input{
  width:100%;
  padding:10px;
  border:none;
  border-radius:8px;
  margin-bottom:15px;
}
.login-card button{
  width:100%;
  padding:10px;
  border:none;
  border-radius:8px;
  background:#00c6ff;
  font-weight:bold;
  cursor:pointer;
}

/* ---------- DASHBOARD ---------- */
#dashboard{
  display:none;
}
.top-bar{
  height:60px;
  padding:0 20px;
  display:flex;
  justify-content:space-between;
  align-items:center;
  background:rgba(255,255,255,0.1);
  backdrop-filter:blur(10px);
}
.logo{
  font-weight:bold;
}
.profile-wrapper{
  position:relative;
}
.profile-circle{
  width:40px;
  height:40px;
  border-radius:50%;
  background:#0072ff;
  display:flex;
  align-items:center;
  justify-content:center;
  cursor:pointer;
}
.profile-menu{
  display:none;
  position:absolute;
  right:0;
  top:50px;
  background:rgba(0,0,0,0.6);
  padding:10px;
  border-radius:10px;
  min-width:150px;
}
.profile-menu p{
  margin-bottom:8px;
}
.profile-menu button{
  width:100%;
  padding:6px;
  border:none;
  border-radius:6px;
  cursor:pointer;
}

/* ---------- TITLE ---------- */
.title{
  text-align:center;
  margin:40px 0;
  font-size:28px;
}
.title span{
  color:#00c6ff;
}

/* ---------- FLOAT LOGIN MSG ---------- */
.login-box-msg{
  position:fixed;
  top:75px;
  right:20px;
  background:rgba(255,255,255,0.15);
  backdrop-filter:blur(12px);
  padding:12px 18px;
  border-radius:10px;
  animation:slideIn 0.4s ease;
}
.login-box-msg.hide{
  opacity:0;
  transform:translateY(-15px);
  pointer-events:none;
}
@keyframes slideIn{
  from{opacity:0; transform:translateX(30px);}
  to{opacity:1; transform:translateX(0);}
}

/* ---------- WIDGETS ---------- */
.widgets{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
  gap:15px;
  padding:20px;
}
.widget{
  background:rgba(255,255,255,0.12);
  padding:20px;
  border-radius:14px;
  text-align:center;
}
</style>
</head>

<body>

<!-- 🔐 LOGIN PAGE -->
<div id="loginPage">
  <div class="login-card">
    <h2>InfiniteSearch Login</h2>
    <input type="text" id="username" placeholder="Enter username">
    <button onclick="login()">Login</button>
  </div>
</div>

<!-- 🌌 DASHBOARD -->
<div id="dashboard">

  <div class="top-bar">
    <div class="logo">InfiniteSearch</div>

    <div class="profile-wrapper">
      <div class="profile-circle" onclick="toggleMenu()">👤</div>
      <div class="profile-menu" id="profileMenu">
        <p id="profileUser"></p>
        <button onclick="logout()">Logout</button>
      </div>
    </div>
  </div>

  <div class="title">
    Welcome to <span>InfiniteSearch</span>
  </div>

  <div id="loginBox" class="login-box-msg">
    Logged in as <b><span id="user"></span></b>
  </div>

  <!-- 📦 WIDGETS -->
  <div class="widgets">
    <div class="widget">🔍 Search Engine</div>
    <div class="widget">📊 Analytics</div>
    <div class="widget">⚙ Settings</div>
    <div class="widget">🌐 Live Status</div>
  </div>

</div>

<script>
/* ---------- AUTH ---------- */
const loggedUser = localStorage.getItem("loggedUser");

if(loggedUser){
  showDashboard(loggedUser);
}

/* LOGIN */
function login(){
  const username=document.getElementById("username").value.trim();
  if(username.length<3){
    alert("Enter valid username");
    return;
  }
  localStorage.setItem("loggedUser",username);
  showDashboard(username);
}

/* SHOW DASHBOARD */
function showDashboard(user){
  document.getElementById("loginPage").style.display="none";
  document.getElementById("dashboard").style.display="block";
  document.getElementById("user").innerText=user;
  document.getElementById("profileUser").innerText="👤 "+user;

  setTimeout(()=>{
    document.getElementById("loginBox").classList.add("hide");
  },8000);

  document.addEventListener("click",()=>{
    document.getElementById("loginBox").classList.add("hide");
  });
}

/* PROFILE MENU */
function toggleMenu(){
  const menu=document.getElementById("profileMenu");
  menu.style.display=menu.style.display==="block"?"none":"block";
}

/* LOGOUT */
function logout(){
  localStorage.removeItem("loggedUser");
  location.reload();
}
</script>

</body>
</html>
