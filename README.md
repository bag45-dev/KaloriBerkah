[index.html](https://github.com/user-attachments/files/28150459/index.html)
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KaloriBerkah - Hitung Kalori, Sehatkan Tubuh, Berkahi Hidup</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Sora:wght@400;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
:root {
  --green: #10B981;
  --green-dark: #059669;
  --green-light: #D1FAE5;
  --orange: #F59E0B;
  --orange-dark: #D97706;
  --orange-light: #FEF3C7;
  --bg: #F8FAFC;
  --card: #FFFFFF;
  --text: #0F172A;
  --text-muted: #64748B;
  --border: #E2E8F0;
  --danger: #EF4444;
  --info: #3B82F6;
  --radius: 16px;
  --shadow: 0 4px 24px rgba(0,0,0,0.08);
  --shadow-lg: 0 8px 48px rgba(0,0,0,0.12);
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Plus Jakarta Sans',sans-serif;background:var(--bg);color:var(--text);line-height:1.6}
/* SCROLLBAR */
::-webkit-scrollbar{width:6px}
::-webkit-scrollbar-track{background:#f1f5f9}
::-webkit-scrollbar-thumb{background:var(--green);border-radius:99px}
/* LAYOUT */
.container{max-width:1200px;margin:0 auto;padding:0 20px}
/* NAV */
nav{background:#fff;border-bottom:1px solid var(--border);position:sticky;top:0;z-index:100;box-shadow:0 2px 12px rgba(0,0,0,0.06)}
.nav-inner{display:flex;align-items:center;justify-content:space-between;height:68px}
.logo{display:flex;align-items:center;gap:10px;text-decoration:none}
.logo-icon{width:38px;height:38px;background:linear-gradient(135deg,var(--green),var(--green-dark));border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:20px}
.logo-text{font-family:'Sora',sans-serif;font-weight:800;font-size:1.2rem;color:var(--text)}
.logo-text span{color:var(--green)}
.nav-links{display:flex;align-items:center;gap:4px}
.nav-links a{text-decoration:none;color:var(--text-muted);font-size:.875rem;font-weight:500;padding:8px 14px;border-radius:8px;transition:.2s}
.nav-links a:hover,.nav-links a.active{background:var(--green-light);color:var(--green-dark)}
.nav-actions{display:flex;align-items:center;gap:10px}
.btn{display:inline-flex;align-items:center;gap:8px;padding:10px 20px;border-radius:10px;font-size:.875rem;font-weight:600;cursor:pointer;border:none;transition:.2s;text-decoration:none;font-family:inherit}
.btn-primary{background:var(--green);color:#fff}
.btn-primary:hover{background:var(--green-dark)}
.btn-orange{background:var(--orange);color:#fff}
.btn-orange:hover{background:var(--orange-dark)}
.btn-outline{background:transparent;color:var(--green);border:2px solid var(--green)}
.btn-outline:hover{background:var(--green-light)}
.btn-danger{background:var(--danger);color:#fff}
.btn-sm{padding:7px 14px;font-size:.8rem}
.btn-lg{padding:14px 28px;font-size:1rem;border-radius:12px}
.hamburger{display:none;flex-direction:column;gap:5px;cursor:pointer;padding:8px;border-radius:8px;background:none;border:none}
.hamburger span{display:block;width:22px;height:2px;background:var(--text);border-radius:2px;transition:.3s}
/* PAGES */
.page{display:none}
.page.active{display:block}
/* HERO */
.hero{background:linear-gradient(135deg,#0F172A 0%,#1E3A2F 40%,#0F2A1E 100%);padding:80px 0 100px;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:-50%;right:-10%;width:600px;height:600px;background:radial-gradient(circle,rgba(16,185,129,.25) 0%,transparent 70%);pointer-events:none}
.hero::after{content:'';position:absolute;bottom:-20%;left:-5%;width:400px;height:400px;background:radial-gradient(circle,rgba(245,158,11,.15) 0%,transparent 70%);pointer-events:none}
.hero-content{position:relative;z-index:2;display:grid;grid-template-columns:1fr 1fr;gap:60px;align-items:center}
.hero-badge{display:inline-flex;align-items:center;gap:8px;background:rgba(16,185,129,.15);border:1px solid rgba(16,185,129,.3);color:#6EE7B7;padding:6px 16px;border-radius:99px;font-size:.8rem;font-weight:600;margin-bottom:24px}
.hero h1{font-family:'Sora',sans-serif;font-size:clamp(2rem,4vw,3.2rem);font-weight:800;color:#fff;line-height:1.15;margin-bottom:16px}
.hero h1 span{color:var(--green)}
.hero p{color:#94A3B8;font-size:1.05rem;margin-bottom:32px;line-height:1.7}
.hero-btns{display:flex;flex-wrap:wrap;gap:12px}
.hero-stats{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-top:40px}
.hero-stat{background:rgba(255,255,255,.07);backdrop-filter:blur(8px);border:1px solid rgba(255,255,255,.1);border-radius:12px;padding:16px 20px}
.hero-stat-num{font-family:'Sora',sans-serif;font-size:1.6rem;font-weight:800;color:#fff}
.hero-stat-label{font-size:.8rem;color:#94A3B8;margin-top:2px}
.hero-visual{position:relative}
.hero-card{background:rgba(255,255,255,.08);backdrop-filter:blur(16px);border:1px solid rgba(255,255,255,.12);border-radius:20px;padding:28px;color:#fff}
.hero-card-title{font-size:.85rem;color:#94A3B8;margin-bottom:16px;display:flex;align-items:center;gap:8px}
.calorie-ring{width:140px;height:140px;margin:0 auto 20px;position:relative;display:flex;align-items:center;justify-content:center}
.calorie-ring svg{position:absolute;top:0;left:0;transform:rotate(-90deg)}
.ring-text{text-align:center;position:relative;z-index:1}
.ring-num{font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800;color:#fff}
.ring-label{font-size:.75rem;color:#94A3B8}
.macro-bars{display:flex;flex-direction:column;gap:10px}
.macro-bar-item{display:flex;align-items:center;gap:12px;font-size:.8rem}
.macro-bar-label{width:70px;color:#94A3B8}
.macro-bar-track{flex:1;height:8px;background:rgba(255,255,255,.1);border-radius:99px;overflow:hidden}
.macro-bar-fill{height:100%;border-radius:99px;transition:width .8s ease}
.macro-bar-val{width:50px;text-align:right;color:#fff;font-weight:600}
/* SECTIONS */
section{padding:80px 0}
.section-label{font-size:.8rem;font-weight:700;color:var(--green);text-transform:uppercase;letter-spacing:.1em;margin-bottom:10px}
.section-title{font-family:'Sora',sans-serif;font-size:clamp(1.6rem,3vw,2.4rem);font-weight:800;color:var(--text);margin-bottom:12px;line-height:1.25}
.section-sub{color:var(--text-muted);font-size:1rem;max-width:560px}
/* CARDS */
.card{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);box-shadow:var(--shadow);padding:28px}
.card-sm{padding:20px}
/* FEATURES */
.features-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:24px;margin-top:48px}
.feature-card{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);padding:28px;transition:.3s;cursor:default}
.feature-card:hover{border-color:var(--green);box-shadow:0 8px 32px rgba(16,185,129,.12);transform:translateY(-4px)}
.feature-icon{width:52px;height:52px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:24px;margin-bottom:16px}
.feature-card h3{font-size:1.05rem;font-weight:700;margin-bottom:8px}
.feature-card p{font-size:.875rem;color:var(--text-muted);line-height:1.6}
/* CALCULATOR */
.calc-section{background:linear-gradient(135deg,#f0fdf4,#fef3c7)}
.calc-grid{display:grid;grid-template-columns:1fr 1fr;gap:40px;align-items:start;margin-top:40px}
.form-group{margin-bottom:20px}
.form-group label{display:block;font-size:.875rem;font-weight:600;color:var(--text);margin-bottom:8px}
.form-group input,.form-group select{width:100%;padding:11px 16px;border:2px solid var(--border);border-radius:10px;font-size:.9rem;font-family:inherit;color:var(--text);background:#fff;transition:.2s}
.form-group input:focus,.form-group select:focus{outline:none;border-color:var(--green);box-shadow:0 0 0 3px rgba(16,185,129,.1)}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:16px}
.result-card{background:#fff;border-radius:var(--radius);border:2px solid var(--green);padding:28px;display:none}
.result-card.show{display:block}
.result-kcal{font-family:'Sora',sans-serif;font-size:3rem;font-weight:800;color:var(--green);line-height:1}
.result-label{color:var(--text-muted);font-size:.9rem;margin-top:4px}
.macro-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-top:20px}
.macro-item{background:var(--bg);border-radius:10px;padding:14px;text-align:center}
.macro-num{font-family:'Sora',sans-serif;font-size:1.4rem;font-weight:700}
.macro-name{font-size:.75rem;color:var(--text-muted);margin-top:2px}
/* LOG PAGE */
.log-layout{display:grid;grid-template-columns:1fr 380px;gap:28px;margin-top:28px}
.search-box{position:relative}
.search-box input{width:100%;padding:12px 16px 12px 44px;border:2px solid var(--border);border-radius:10px;font-size:.9rem;font-family:inherit;background:#fff}
.search-box input:focus{outline:none;border-color:var(--green)}
.search-box .search-icon{position:absolute;left:14px;top:50%;transform:translateY(-50%);color:var(--text-muted)}
.autocomplete-list{position:absolute;top:calc(100% + 4px);left:0;right:0;background:#fff;border:1px solid var(--border);border-radius:10px;box-shadow:var(--shadow-lg);z-index:50;max-height:240px;overflow-y:auto;display:none}
.autocomplete-list.show{display:block}
.ac-item{padding:10px 16px;cursor:pointer;display:flex;align-items:center;justify-content:space-between;font-size:.875rem;transition:.15s}
.ac-item:hover{background:var(--green-light)}
.ac-kcal{color:var(--green);font-weight:600;font-size:.8rem}
.log-table{width:100%;border-collapse:collapse;margin-top:16px}
.log-table th{text-align:left;font-size:.75rem;font-weight:700;color:var(--text-muted);text-transform:uppercase;letter-spacing:.05em;padding:8px 12px;border-bottom:2px solid var(--border)}
.log-table td{padding:10px 12px;border-bottom:1px solid var(--border);font-size:.875rem}
.log-table tr:hover td{background:#f8fafc}
.del-btn{background:none;border:none;color:var(--text-muted);cursor:pointer;padding:4px 8px;border-radius:6px;font-size:1rem;transition:.2s}
.del-btn:hover{background:#fee2e2;color:var(--danger)}
.progress-container{margin:16px 0}
.progress-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;font-size:.875rem;font-weight:600}
.progress-bar{height:14px;background:var(--border);border-radius:99px;overflow:hidden}
.progress-fill{height:100%;background:linear-gradient(90deg,var(--green),#34D399);border-radius:99px;transition:width .5s ease}
.progress-fill.warning{background:linear-gradient(90deg,var(--orange),#FCD34D)}
.progress-fill.danger{background:linear-gradient(90deg,var(--danger),#F87171)}
.daily-summary{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:16px}
.summary-item{background:var(--bg);border-radius:10px;padding:14px;text-align:center}
.summary-num{font-family:'Sora',sans-serif;font-size:1.5rem;font-weight:700}
.summary-label{font-size:.75rem;color:var(--text-muted)}
/* MENU PAGE */
.menu-tabs{display:flex;gap:8px;margin-bottom:28px;flex-wrap:wrap}
.menu-tab{padding:9px 20px;border-radius:99px;font-size:.875rem;font-weight:600;cursor:pointer;border:2px solid var(--border);background:transparent;color:var(--text-muted);transition:.2s;font-family:inherit}
.menu-tab.active{background:var(--green);color:#fff;border-color:var(--green)}
.menu-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:20px}
.menu-card{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);overflow:hidden;transition:.3s}
.menu-card:hover{border-color:var(--green);box-shadow:var(--shadow-lg);transform:translateY(-3px)}
.menu-card-img{height:160px;background:linear-gradient(135deg,#e0f2fe,#d1fae5);display:flex;align-items:center;justify-content:center;font-size:56px}
.menu-card-body{padding:16px}
.menu-card-title{font-weight:700;margin-bottom:6px}
.menu-card-kcal{font-size:.8rem;color:var(--green);font-weight:700;background:var(--green-light);display:inline-block;padding:3px 10px;border-radius:99px;margin-bottom:10px}
.menu-card-time{font-size:.75rem;color:var(--text-muted)}
.tag{display:inline-block;padding:3px 10px;border-radius:99px;font-size:.72rem;font-weight:600}
.tag-green{background:var(--green-light);color:var(--green-dark)}
.tag-orange{background:var(--orange-light);color:var(--orange-dark)}
.tag-blue{background:#DBEAFE;color:#1D4ED8}
/* BLOG */
.blog-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(320px,1fr));gap:24px}
.blog-card{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);overflow:hidden;transition:.3s;cursor:pointer}
.blog-card:hover{border-color:var(--green);box-shadow:var(--shadow-lg);transform:translateY(-3px)}
.blog-img{height:180px;display:flex;align-items:center;justify-content:center;font-size:64px}
.blog-body{padding:20px}
.blog-cat{font-size:.72rem;font-weight:700;color:var(--green);text-transform:uppercase;letter-spacing:.08em;margin-bottom:10px}
.blog-title{font-weight:700;font-size:1.05rem;line-height:1.4;margin-bottom:8px}
.blog-excerpt{font-size:.875rem;color:var(--text-muted);line-height:1.6}
.blog-meta{font-size:.75rem;color:var(--text-muted);margin-top:12px;display:flex;align-items:center;gap:12px}
/* FORUM */
.forum-list{display:flex;flex-direction:column;gap:16px}
.forum-item{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);padding:20px;display:flex;gap:16px;cursor:pointer;transition:.2s}
.forum-item:hover{border-color:var(--green);box-shadow:var(--shadow)}
.forum-avatar{width:44px;height:44px;border-radius:50%;background:linear-gradient(135deg,var(--green),var(--green-dark));display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;font-size:.9rem;flex-shrink:0}
.forum-content{flex:1}
.forum-title{font-weight:700;margin-bottom:4px}
.forum-preview{font-size:.875rem;color:var(--text-muted)}
.forum-footer{display:flex;gap:16px;margin-top:10px;font-size:.75rem;color:var(--text-muted)}
/* DONASI PAGE */
.donasi-hero{background:linear-gradient(135deg,#064E3B,#065F46);color:#fff;border-radius:20px;padding:48px;text-align:center;margin-bottom:40px}
.donasi-hero h2{font-family:'Sora',sans-serif;font-size:2rem;font-weight:800;margin-bottom:12px}
.donasi-hero p{color:#A7F3D0;font-size:1rem;max-width:500px;margin:0 auto 28px}
.donasi-counter{display:inline-flex;align-items:center;gap:8px;background:rgba(255,255,255,.1);padding:12px 24px;border-radius:12px;margin-bottom:28px}
.donasi-counter-num{font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800}
.donasi-counter-label{font-size:.8rem;color:#A7F3D0}
.nominal-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:12px;margin-bottom:20px}
.nominal-btn{padding:14px;border-radius:10px;border:2px solid var(--border);background:#fff;font-size:.9rem;font-weight:600;cursor:pointer;transition:.2s;font-family:inherit;color:var(--text)}
.nominal-btn:hover,.nominal-btn.active{border-color:var(--green);background:var(--green-light);color:var(--green-dark)}
.donatur-list{display:flex;flex-direction:column;gap:10px;margin-top:24px}
.donatur-item{display:flex;align-items:center;gap:12px;background:var(--bg);border-radius:10px;padding:12px 16px;font-size:.875rem}
.donatur-avatar{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,var(--orange),var(--orange-dark));display:flex;align-items:center;justify-content:center;color:#fff;font-size:.8rem;font-weight:700}
.donatur-name{font-weight:600}
.donatur-amount{color:var(--green);font-weight:700;margin-left:auto}
.donatur-time{color:var(--text-muted);font-size:.75rem}
/* ADMIN */
.admin-layout{display:grid;grid-template-columns:260px 1fr;min-height:100vh}
.admin-sidebar{background:#0F172A;color:#fff;padding:24px 0;display:flex;flex-direction:column}
.admin-logo{padding:0 24px 24px;border-bottom:1px solid rgba(255,255,255,.1);margin-bottom:16px}
.admin-logo .logo-text{color:#fff}
.admin-nav a{display:flex;align-items:center;gap:12px;padding:11px 24px;color:#94A3B8;text-decoration:none;font-size:.875rem;font-weight:500;transition:.2s;border-left:3px solid transparent}
.admin-nav a:hover,.admin-nav a.active{color:#fff;background:rgba(255,255,255,.06);border-left-color:var(--green)}
.admin-nav a span{font-size:1.1rem}
.admin-main{flex:1;padding:28px;background:var(--bg);overflow-y:auto}
.admin-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:28px}
.admin-header h1{font-family:'Sora',sans-serif;font-size:1.5rem;font-weight:700}
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:20px;margin-bottom:28px}
.stat-card{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);padding:20px}
.stat-card-icon{font-size:1.8rem;margin-bottom:10px}
.stat-card-val{font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800;color:var(--text)}
.stat-card-label{font-size:.8rem;color:var(--text-muted);margin-top:2px}
.admin-table{width:100%;border-collapse:collapse;font-size:.875rem}
.admin-table th{background:#f1f5f9;text-align:left;padding:10px 14px;font-size:.75rem;font-weight:700;color:var(--text-muted);text-transform:uppercase}
.admin-table td{padding:12px 14px;border-bottom:1px solid var(--border)}
.admin-table tr:hover td{background:#f8fafc}
/* SETTINGS */
.settings-layout{display:grid;grid-template-columns:220px 1fr;gap:28px;margin-top:28px}
.settings-nav{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);padding:8px;height:fit-content}
.settings-nav a{display:flex;align-items:center;gap:10px;padding:10px 14px;border-radius:8px;text-decoration:none;color:var(--text-muted);font-size:.875rem;font-weight:500;transition:.2s}
.settings-nav a:hover,.settings-nav a.active{background:var(--green-light);color:var(--green-dark)}
/* MODALS */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.5);backdrop-filter:blur(4px);z-index:1000;display:flex;align-items:center;justify-content:center;padding:20px;opacity:0;pointer-events:none;transition:.3s}
.modal-overlay.show{opacity:1;pointer-events:all}
.modal{background:#fff;border-radius:20px;max-width:520px;width:100%;max-height:90vh;overflow-y:auto;transform:scale(.95);transition:.3s;box-shadow:0 20px 80px rgba(0,0,0,.2)}
.modal-overlay.show .modal{transform:scale(1)}
.modal-header{padding:24px 28px 16px;border-bottom:1px solid var(--border);display:flex;align-items:flex-start;justify-content:space-between}
.modal-title{font-family:'Sora',sans-serif;font-weight:700;font-size:1.2rem}
.modal-close{background:none;border:none;cursor:pointer;color:var(--text-muted);font-size:1.4rem;padding:4px;line-height:1;margin-top:-2px}
.modal-body{padding:24px 28px}
.modal-footer{padding:16px 28px 24px;display:flex;gap:12px;justify-content:flex-end}
/* TESTIMONIALS */
.testimonial-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:20px;margin-top:40px}
.testimonial-card{background:var(--card);border-radius:var(--radius);border:1px solid var(--border);padding:24px}
.testimonial-stars{color:var(--orange);font-size:1rem;margin-bottom:12px}
.testimonial-text{font-size:.9rem;color:var(--text-muted);line-height:1.7;margin-bottom:16px;font-style:italic}
.testimonial-author{display:flex;align-items:center;gap:12px}
.testimonial-avatar{width:42px;height:42px;border-radius:50%;background:linear-gradient(135deg,var(--green),var(--green-dark));display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700}
.testimonial-name{font-weight:700;font-size:.9rem}
.testimonial-loc{font-size:.75rem;color:var(--text-muted)}
/* BADGES */
.badge-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:16px}
.badge-item{background:var(--card);border-radius:12px;border:1px solid var(--border);padding:16px;text-align:center;transition:.2s}
.badge-item.earned{border-color:var(--orange)}
.badge-item.earned .badge-icon{filter:none}
.badge-icon{font-size:2.5rem;margin-bottom:8px;filter:grayscale(1) opacity(.4)}
.badge-name{font-size:.8rem;font-weight:700;margin-bottom:4px}
.badge-desc{font-size:.72rem;color:var(--text-muted)}
/* TOAST */
.toast-container{position:fixed;bottom:24px;right:24px;z-index:9999;display:flex;flex-direction:column;gap:8px}
.toast{background:#fff;border-radius:12px;box-shadow:0 8px 32px rgba(0,0,0,.15);padding:14px 18px;display:flex;align-items:center;gap:12px;font-size:.875rem;font-weight:500;border-left:4px solid var(--green);transform:translateX(120%);transition:.4s cubic-bezier(.175,.885,.32,1.275);max-width:320px}
.toast.show{transform:translateX(0)}
.toast.error{border-left-color:var(--danger)}
.toast.warning{border-left-color:var(--orange)}
/* FOOTER */
footer{background:#0F172A;color:#94A3B8;padding:60px 0 30px}
.footer-grid{display:grid;grid-template-columns:2fr 1fr 1fr 1fr;gap:40px;margin-bottom:40px}
.footer-brand p{font-size:.875rem;line-height:1.7;margin-top:12px;max-width:260px}
.footer-col h4{font-weight:700;color:#fff;margin-bottom:16px;font-size:.9rem}
.footer-col a{display:block;color:#94A3B8;text-decoration:none;font-size:.875rem;margin-bottom:8px;transition:.2s}
.footer-col a:hover{color:var(--green)}
.footer-bottom{border-top:1px solid rgba(255,255,255,.08);padding-top:24px;display:flex;align-items:center;justify-content:space-between;font-size:.8rem}
/* WATER TRACKER */
.water-tracker{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
.water-glass{width:36px;height:36px;border-radius:8px;border:2px solid var(--info);background:transparent;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:1.1rem;transition:.2s}
.water-glass.filled{background:#DBEAFE;border-color:var(--info)}
/* GAMIFIKASI */
.points-bar{display:flex;align-items:center;gap:12px;background:var(--orange-light);border:1px solid var(--orange);border-radius:10px;padding:12px 16px;margin-bottom:20px}
.points-num{font-family:'Sora',sans-serif;font-size:1.4rem;font-weight:800;color:var(--orange-dark)}
/* CHART CONTAINER */
.chart-wrapper{position:relative;height:280px}
/* LOGIN ADMIN */
.login-page{min-height:100vh;background:linear-gradient(135deg,#0F172A,#1E3A2F);display:flex;align-items:center;justify-content:center;padding:20px}
.login-card{background:#fff;border-radius:20px;padding:40px;width:100%;max-width:400px;box-shadow:var(--shadow-lg)}
.login-card h2{font-family:'Sora',sans-serif;font-size:1.6rem;font-weight:800;text-align:center;margin-bottom:6px}
.login-card p{color:var(--text-muted);text-align:center;font-size:.875rem;margin-bottom:28px}
/* RESPONSIVE */
@media(max-width:768px){
  .hero-content{grid-template-columns:1fr}
  .hero-visual{display:none}
  .calc-grid{grid-template-columns:1fr}
  .log-layout{grid-template-columns:1fr}
  .admin-layout{grid-template-columns:1fr}
  .admin-sidebar{display:none}
  .footer-grid{grid-template-columns:1fr 1fr}
  .nav-links{display:none}
  .hamburger{display:flex}
  .mobile-menu{display:flex;flex-direction:column;gap:4px;padding:16px;border-top:1px solid var(--border);background:#fff}
  .mobile-menu a{padding:12px 16px;border-radius:8px;text-decoration:none;color:var(--text);font-weight:500}
  .settings-layout{grid-template-columns:1fr}
  .settings-nav{display:none}
  .form-row{grid-template-columns:1fr}
  .hero-stats{grid-template-columns:1fr 1fr}
}
@media(max-width:480px){
  .footer-grid{grid-template-columns:1fr}
  .macro-grid{grid-template-columns:repeat(3,1fr)}
  .nominal-grid{grid-template-columns:repeat(2,1fr)}
}
.hidden{display:none!important}
.text-center{text-align:center}
.mt-4{margin-top:16px}
.mt-6{margin-top:24px}
.mt-8{margin-top:32px}
.mb-4{margin-bottom:16px}
.mb-6{margin-bottom:24px}
.flex{display:flex}
.items-center{align-items:center}
.justify-between{justify-content:space-between}
.gap-2{gap:8px}
.gap-4{gap:16px}
.font-bold{font-weight:700}
.text-green{color:var(--green)}
.text-orange{color:var(--orange)}
.text-muted{color:var(--text-muted)}
.text-sm{font-size:.875rem}
.text-xs{font-size:.75rem}
.w-full{width:100%}
.divider{height:1px;background:var(--border);margin:20px 0}
</style>
</head>
<body>

<!-- NAVIGATION -->
<nav id="mainNav">
  <div class="container">
    <div class="nav-inner">
      <a href="#" class="logo" onclick="showPage('home')">
        <div class="logo-icon">🥗</div>
        <div class="logo-text">Kalori<span>Berkah</span></div>
      </a>
      <div class="nav-links">
        <a href="#" onclick="showPage('home')" class="active" id="nav-home">Beranda</a>
        <a href="#" onclick="showPage('log')" id="nav-log">Log Harian</a>
        <a href="#" onclick="showPage('menu')" id="nav-menu">Menu Sehat</a>
        <a href="#" onclick="showPage('blog')" id="nav-blog">Blog</a>
        <a href="#" onclick="showPage('forum')" id="nav-forum">Forum</a>
        <a href="#" onclick="showPage('donasi')" id="nav-donasi">Donasi</a>
      </div>
      <div class="nav-actions">
        <button class="btn btn-orange btn-sm" onclick="openDonasiModal()">🌟 Donasi Berkah</button>
        <a href="#" onclick="showAdminLogin()" class="btn btn-outline btn-sm">Admin</a>
        <button class="hamburger" onclick="toggleMobileMenu()">
          <span></span><span></span><span></span>
        </button>
      </div>
    </div>
    <div id="mobileMenu" class="mobile-menu hidden">
      <a href="#" onclick="showPage('home');toggleMobileMenu()">🏠 Beranda</a>
      <a href="#" onclick="showPage('log');toggleMobileMenu()">📋 Log Harian</a>
      <a href="#" onclick="showPage('menu');toggleMobileMenu()">🍽️ Menu Sehat</a>
      <a href="#" onclick="showPage('blog');toggleMobileMenu()">📚 Blog</a>
      <a href="#" onclick="showPage('forum');toggleMobileMenu()">💬 Forum</a>
      <a href="#" onclick="showPage('donasi');toggleMobileMenu()">💝 Donasi</a>
      <a href="#" onclick="showPage('settings');toggleMobileMenu()">⚙️ Pengaturan</a>
    </div>
  </div>
</nav>

<!-- TOAST CONTAINER -->
<div class="toast-container" id="toastContainer"></div>

<!-- ===== PAGES ===== -->

<!-- HOME PAGE -->
<div id="page-home" class="page active">
  <!-- HERO -->
  <section class="hero">
    <div class="container">
      <div class="hero-content">
        <div>
          <div class="hero-badge">🌿 Platform Kesehatan & Berbagi</div>
          <h1>Hitung Kalori,<br><span>Sehatkan Tubuh,</span><br>Berkahi Hidup</h1>
          <p>Kalkulator kalori pintar dengan menu sehat ala Indonesia, tracking harian, dan fitur donasi berkah — semua dalam satu platform.</p>
          <div class="hero-btns">
            <button class="btn btn-primary btn-lg" onclick="scrollToCalc()">🧮 Hitung Kalori Sekarang</button>
            <button class="btn btn-orange btn-lg" onclick="openDonasiModal()">🌟 Donasi Berkah</button>
          </div>
          <div class="hero-stats">
            <div class="hero-stat">
              <div class="hero-stat-num" id="statCalc">50.000+</div>
              <div class="hero-stat-label">Kalori Dihitung</div>
            </div>
            <div class="hero-stat">
              <div class="hero-stat-num" id="statDonasi">Rp 125Jt+</div>
              <div class="hero-stat-label">Donasi Terkumpul</div>
            </div>
            <div class="hero-stat">
              <div class="hero-stat-num">10.000+</div>
              <div class="hero-stat-label">Menu Dipilih</div>
            </div>
            <div class="hero-stat">
              <div class="hero-stat-num">5.000+</div>
              <div class="hero-stat-label">User Aktif</div>
            </div>
          </div>
        </div>
        <div class="hero-visual">
          <div class="hero-card">
            <div class="hero-card-title">🎯 Tracking Harian Anda</div>
            <div class="calorie-ring">
              <svg width="140" height="140" viewBox="0 0 140 140">
                <circle cx="70" cy="70" r="58" fill="none" stroke="rgba(255,255,255,.1)" stroke-width="12"/>
                <circle cx="70" cy="70" r="58" fill="none" stroke="#10B981" stroke-width="12" stroke-dasharray="364" stroke-dashoffset="110" stroke-linecap="round"/>
              </svg>
              <div class="ring-text">
                <div class="ring-num">1,450</div>
                <div class="ring-label">dari 1,800 kcal</div>
              </div>
            </div>
            <div class="macro-bars">
              <div class="macro-bar-item">
                <div class="macro-bar-label">Protein</div>
                <div class="macro-bar-track"><div class="macro-bar-fill" style="width:75%;background:#34D399"></div></div>
                <div class="macro-bar-val">82g</div>
              </div>
              <div class="macro-bar-item">
                <div class="macro-bar-label">Karbo</div>
                <div class="macro-bar-track"><div class="macro-bar-fill" style="width:60%;background:#F59E0B"></div></div>
                <div class="macro-bar-val">165g</div>
              </div>
              <div class="macro-bar-item">
                <div class="macro-bar-label">Lemak</div>
                <div class="macro-bar-track"><div class="macro-bar-fill" style="width:50%;background:#60A5FA"></div></div>
                <div class="macro-bar-val">42g</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- FEATURES -->
  <section>
    <div class="container">
      <div class="text-center">
        <div class="section-label">Kenapa KaloriBerkah?</div>
        <h2 class="section-title">Semua yang Anda Butuhkan</h2>
        <p class="section-sub" style="margin:0 auto">Platform lengkap untuk perjalanan hidup sehat Anda dengan sentuhan berkah yang bermakna.</p>
      </div>
      <div class="features-grid">
        <div class="feature-card">
          <div class="feature-icon" style="background:#D1FAE5">🧮</div>
          <h3>Kalkulator Akurat</h3>
          <p>Hitung kebutuhan kalori harian dengan rumus Mifflin-St Jeor yang terstandarisasi secara ilmiah.</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon" style="background:#FEF3C7">🍽️</div>
          <h3>Menu Rekomendasi</h3>
          <p>Dapatkan 3 paket menu sehari penuh sesuai target kalori Anda, dengan resep mudah dan bahan lokal.</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon" style="background:#DBEAFE">📊</div>
          <h3>Tracking Harian</h3>
          <p>Log konsumsi makanan dengan mudah, lihat progress real-time, dan grafik perkembangan mingguan.</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon" style="background:#FCE7F3">🌟</div>
          <h3>Donasi Berkah</h3>
          <p>Setiap langkah sehat Anda bisa menjadi berkah bagi yang membutuhkan melalui fitur donasi terintegrasi.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- CALCULATOR SECTION -->
  <section class="calc-section" id="calcSection">
    <div class="container">
      <div class="section-label">Kalkulator Kalori</div>
      <h2 class="section-title">Berapa Kebutuhan Kalori Anda?</h2>
      <div class="calc-grid">
        <div class="card">
          <h3 style="margin-bottom:20px;font-size:1.1rem">📝 Isi Data Anda</h3>
          <div class="form-group">
            <label>Nama (opsional)</label>
            <input type="text" id="calcName" placeholder="Masukkan nama Anda">
          </div>
          <div class="form-row">
            <div class="form-group">
              <label>Usia (tahun) *</label>
              <input type="number" id="calcAge" placeholder="25" min="10" max="100">
            </div>
            <div class="form-group">
              <label>Jenis Kelamin *</label>
              <select id="calcGender">
                <option value="">Pilih...</option>
                <option value="male">Laki-laki</option>
                <option value="female">Perempuan</option>
              </select>
            </div>
          </div>
          <div class="form-row">
            <div class="form-group">
              <label>Berat Badan (kg) *</label>
              <input type="number" id="calcWeight" placeholder="65" min="20" max="300">
            </div>
            <div class="form-group">
              <label>Tinggi Badan (cm) *</label>
              <input type="number" id="calcHeight" placeholder="170" min="100" max="250">
            </div>
          </div>
          <div class="form-group">
            <label>Tingkat Aktivitas *</label>
            <select id="calcActivity">
              <option value="">Pilih...</option>
              <option value="1.2">Sedentary (Jarang olahraga)</option>
              <option value="1.375">Ringan (1-3x/minggu)</option>
              <option value="1.55">Sedang (3-5x/minggu)</option>
              <option value="1.725">Berat (6-7x/minggu)</option>
              <option value="1.9">Sangat Berat (2x/hari)</option>
            </select>
          </div>
          <div class="form-group">
            <label>Tujuan *</label>
            <select id="calcGoal">
              <option value="">Pilih...</option>
              <option value="lose">Turun Berat Badan (-500 kcal)</option>
              <option value="maintain">Mempertahankan Berat Badan</option>
              <option value="gain">Naik Berat Badan (+500 kcal)</option>
            </select>
          </div>
          <button class="btn btn-primary w-full btn-lg" onclick="calculateCalories()">🧮 Hitung Kalori Sekarang</button>
        </div>
        <div>
          <div class="result-card" id="resultCard">
            <div class="text-sm text-muted mb-4" id="resultName"></div>
            <div class="result-kcal" id="resultKcal">0</div>
            <div class="result-label">kcal/hari yang Anda butuhkan</div>
            <div class="divider"></div>
            <div class="text-sm font-bold mb-4" style="color:var(--text)">📊 Breakdown Makronutrien</div>
            <div class="macro-grid">
              <div class="macro-item">
                <div class="macro-num text-green" id="rProtein">0g</div>
                <div class="macro-name">Protein</div>
              </div>
              <div class="macro-item">
                <div class="macro-num text-orange" id="rKarbo">0g</div>
                <div class="macro-name">Karbohidrat</div>
              </div>
              <div class="macro-item">
                <div class="macro-num" style="color:var(--info)" id="rLemak">0g</div>
                <div class="macro-name">Lemak</div>
              </div>
            </div>
            <div class="divider"></div>
            <div id="resultDetail" style="font-size:.85rem;color:var(--text-muted);line-height:1.7"></div>
            <div class="mt-4 flex gap-2">
              <button class="btn btn-primary btn-sm" onclick="showPage('log')">📋 Mulai Log Harian</button>
              <button class="btn btn-outline btn-sm" onclick="showPage('menu')">🍽️ Lihat Menu</button>
            </div>
          </div>
          <div id="calcPlaceholder" class="card" style="text-align:center;padding:48px 28px">
            <div style="font-size:64px;margin-bottom:16px">🥗</div>
            <h3 style="margin-bottom:8px">Isi form di samping</h3>
            <p style="color:var(--text-muted);font-size:.9rem">Hasil kalori dan rekomendasi menu akan muncul di sini</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- TESTIMONIALS -->
  <section>
    <div class="container">
      <div class="section-label">Testimoni</div>
      <h2 class="section-title">Kata Mereka yang Telah Berhasil</h2>
      <div class="testimonial-grid">
        <div class="testimonial-card">
          <div class="testimonial-stars">★★★★★</div>
          <p class="testimonial-text">"Alhamdulillah, sejak pakai KaloriBerkah berat badan turun 5kg dalam 2 bulan. Saya juga jadi rutin donasi setiap minggu. Aplikasi yang penuh berkah!"</p>
          <div class="testimonial-author">
            <div class="testimonial-avatar">SA</div>
            <div>
              <div class="testimonial-name">Sara Amalia</div>
              <div class="testimonial-loc">📍 Bandung</div>
            </div>
          </div>
        </div>
        <div class="testimonial-card">
          <div class="testimonial-stars">★★★★★</div>
          <p class="testimonial-text">"Menu rekomendasinya cocok banget untuk lidah Indonesia. Tidak ribet, bahannya mudah dicari, dan kalorinya pas. Praktis banget!"</p>
          <div class="testimonial-author">
            <div class="testimonial-avatar">AR</div>
            <div>
              <div class="testimonial-name">Ahmad Rizki</div>
              <div class="testimonial-loc">📍 Jakarta</div>
            </div>
          </div>
        </div>
        <div class="testimonial-card">
          <div class="testimonial-stars">★★★★★</div>
          <p class="testimonial-text">"Fitur tracking hariannya membantu saya lebih sadar dengan apa yang saya makan. Database makanannya lengkap, ada banyak makanan lokal!"</p>
          <div class="testimonial-author">
            <div class="testimonial-avatar">DW</div>
            <div>
              <div class="testimonial-name">Dewi Wijaya</div>
              <div class="testimonial-loc">📍 Surabaya</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- DONASI CTA -->
  <section style="background:linear-gradient(135deg,#064E3B,#065F46);padding:60px 0">
    <div class="container text-center">
      <div style="font-size:3rem;margin-bottom:16px">💝</div>
      <h2 style="font-family:'Sora',sans-serif;font-size:2rem;font-weight:800;color:#fff;margin-bottom:12px">Sehatkan Tubuh, Berkahi Hidup</h2>
      <p style="color:#A7F3D0;max-width:480px;margin:0 auto 28px;line-height:1.7">Setiap kalori yang Anda hitung adalah langkah menuju kesehatan. Setiap donasi yang Anda berikan adalah berkah untuk mereka yang membutuhkan.</p>
      <button class="btn btn-orange btn-lg" onclick="openDonasiModal()">🌟 Donasi Berkah Sekarang</button>
    </div>
  </section>
</div>

<!-- LOG HARIAN PAGE -->
<div id="page-log" class="page">
  <div class="container" style="padding-top:32px;padding-bottom:60px">
    <div class="flex items-center justify-between mb-4">
      <div>
        <div class="section-label">Tracking</div>
        <h1 class="section-title" style="margin-bottom:4px">Log Konsumsi Harian</h1>
        <p class="text-muted text-sm" id="logDate"></p>
      </div>
      <div class="flex gap-2">
        <button class="btn btn-outline btn-sm" onclick="exportLogPDF()">📥 Export PDF</button>
        <button class="btn btn-primary btn-sm" onclick="clearTodayLog()">🗑️ Reset Hari Ini</button>
      </div>
    </div>
    
    <!-- POINTS BAR -->
    <div class="points-bar">
      <span style="font-size:1.5rem">🏆</span>
      <div>
        <div class="points-num" id="userPoints">0 Poin</div>
        <div style="font-size:.75rem;color:var(--orange-dark)">Level: <span id="userLevel">Pemula</span></div>
      </div>
      <div style="margin-left:auto;display:flex;gap:8px">
        <span class="tag tag-green" id="badge1">🌱 Pemula</span>
        <span class="tag tag-orange hidden" id="badge2">🔥 7 Hari</span>
        <span class="tag" style="background:#DBEAFE;color:#1E40AF" id="badge3 hidden">💝 Donatur</span>
      </div>
    </div>

    <div class="log-layout">
      <div>
        <!-- PROGRESS -->
        <div class="card mb-4">
          <div class="flex items-center justify-between mb-4">
            <h3 style="font-size:1rem;font-weight:700">📊 Progress Kalori Hari Ini</h3>
            <span class="text-sm text-muted" id="logProgressText">0 / 1800 kcal</span>
          </div>
          <div class="progress-container">
            <div class="progress-bar">
              <div class="progress-fill" id="progressFill" style="width:0%"></div>
            </div>
            <div class="flex justify-between mt-2 text-xs text-muted">
              <span>0 kcal</span>
              <span id="progressPct">0%</span>
              <span id="progressTarget">Target: 1800 kcal</span>
            </div>
          </div>
          <div class="daily-summary">
            <div class="summary-item">
              <div class="summary-num text-green" id="totalConsumed">0</div>
              <div class="summary-label">kcal Dikonsumsi</div>
            </div>
            <div class="summary-item">
              <div class="summary-num text-orange" id="totalRemaining">1800</div>
              <div class="summary-label">kcal Tersisa</div>
            </div>
            <div class="summary-item">
              <div class="summary-num" style="color:var(--info)" id="totalProtein">0g</div>
              <div class="summary-label">Protein</div>
            </div>
            <div class="summary-item">
              <div class="summary-num" style="color:#8B5CF6" id="totalKarbo">0g</div>
              <div class="summary-label">Karbohidrat</div>
            </div>
          </div>
        </div>

        <!-- INPUT MAKANAN -->
        <div class="card mb-4">
          <h3 style="font-size:1rem;font-weight:700;margin-bottom:16px">➕ Tambah Makanan/Minuman</h3>
          <div class="form-row">
            <div class="form-group" style="margin-bottom:0;position:relative">
              <label>Nama Makanan/Minuman</label>
              <div class="search-box">
                <span class="search-icon">🔍</span>
                <input type="text" id="foodSearch" placeholder="Cari makanan..." oninput="searchFood(this.value)" autocomplete="off">
                <div class="autocomplete-list" id="autocompleteList"></div>
              </div>
            </div>
            <div class="form-group" style="margin-bottom:0">
              <label>Kategori</label>
              <select id="mealCategory">
                <option value="sarapan">🌅 Sarapan</option>
                <option value="siang">☀️ Makan Siang</option>
                <option value="malam">🌙 Makan Malam</option>
                <option value="snack">🍪 Snack</option>
                <option value="minuman">☕ Minuman</option>
              </select>
            </div>
          </div>
          <div class="form-row mt-4">
            <div class="form-group" style="margin-bottom:0">
              <label>Porsi (gram/ml)</label>
              <input type="number" id="foodPortion" placeholder="100" min="1" value="100">
            </div>
            <div class="form-group" style="margin-bottom:0">
              <label>Kalori (otomatis)</label>
              <input type="number" id="foodKcal" placeholder="0" readonly style="background:#f1f5f9">
            </div>
          </div>
          <div id="selectedFoodInfo" class="hidden mt-4" style="background:var(--green-light);border-radius:10px;padding:12px 16px;font-size:.875rem">
            <strong id="selectedFoodName"></strong> — <span id="selectedFoodDetail"></span>
          </div>
          <button class="btn btn-primary w-full mt-4" onclick="addFoodToLog()">➕ Tambah ke Log</button>
        </div>

        <!-- LOG TABLE -->
        <div class="card">
          <h3 style="font-size:1rem;font-weight:700;margin-bottom:16px">🍽️ Log Makanan Hari Ini</h3>
          <div id="logByCategory"></div>
          <div id="emptyLog" class="text-center" style="padding:32px;color:var(--text-muted)">
            <div style="font-size:3rem;margin-bottom:12px">🍽️</div>
            <p>Belum ada makanan yang dicatat. Mulai tambahkan!</p>
          </div>
        </div>
      </div>

      <!-- SIDEBAR -->
      <div>
        <!-- WATER TRACKER -->
        <div class="card mb-4">
          <h3 style="font-size:1rem;font-weight:700;margin-bottom:4px">💧 Tracker Minum Air</h3>
          <p class="text-xs text-muted mb-4">Target: 8 gelas / hari</p>
          <div class="water-tracker" id="waterTracker"></div>
          <p class="text-xs text-muted mt-2" id="waterCount">0 dari 8 gelas</p>
        </div>

        <!-- WEEKLY CHART -->
        <div class="card mb-4">
          <h3 style="font-size:1rem;font-weight:700;margin-bottom:16px">📈 Grafik 7 Hari</h3>
          <div class="chart-wrapper">
            <canvas id="weeklyChart"></canvas>
          </div>
        </div>

        <!-- MAKRO CHART -->
        <div class="card mb-4">
          <h3 style="font-size:1rem;font-weight:700;margin-bottom:16px">🥧 Breakdown Makro</h3>
          <div class="chart-wrapper" style="height:200px">
            <canvas id="macroChart"></canvas>
          </div>
        </div>

        <!-- TIPS -->
        <div class="card" style="background:var(--green-light);border-color:var(--green)">
          <h3 style="font-size:.9rem;font-weight:700;margin-bottom:10px;color:var(--green-dark)">💡 Tips Personal</h3>
          <p class="text-sm" style="color:var(--green-dark);line-height:1.6" id="personalTip">Isi kalkulator di beranda untuk mendapatkan tips personal berdasarkan profil Anda!</p>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- MENU PAGE -->
<div id="page-menu" class="page">
  <div class="container" style="padding-top:32px;padding-bottom:60px">
    <div class="section-label">Rekomendasi</div>
    <h1 class="section-title">Menu Sehat Harian</h1>
    <p class="text-muted mb-6">Pilih paket menu sesuai tujuan kesehatan Anda. Semua resep mudah dibuat!</p>
    
    <div class="menu-tabs">
      <button class="menu-tab active" onclick="switchMenuTab(this,'rendah')">🥗 Rendah Kalori</button>
      <button class="menu-tab" onclick="switchMenuTab(this,'seimbang')">⚖️ Seimbang</button>
      <button class="menu-tab" onclick="switchMenuTab(this,'tinggi')">💪 Tinggi Kalori</button>
    </div>

    <div id="menuContent"></div>
  </div>
</div>

<!-- BLOG PAGE -->
<div id="page-blog" class="page">
  <div class="container" style="padding-top:32px;padding-bottom:60px">
    <div id="blogList">
      <div class="section-label">Edukasi Kesehatan</div>
      <h1 class="section-title">Blog & Artikel</h1>
      <p class="text-muted mb-6">Temukan tips, resep, dan panduan hidup sehat berbasis sains.</p>
      <div class="blog-grid" id="blogGrid"></div>
    </div>
    <div id="blogDetail" class="hidden">
      <button class="btn btn-outline btn-sm mb-6" onclick="backToBlogList()">← Kembali ke Blog</button>
      <div id="blogDetailContent"></div>
    </div>
  </div>
</div>

<!-- FORUM PAGE -->
<div id="page-forum" class="page">
  <div class="container" style="padding-top:32px;padding-bottom:60px">
    <div class="flex items-center justify-between mb-6">
      <div>
        <div class="section-label">Komunitas</div>
        <h1 class="section-title" style="margin-bottom:0">Forum Diskusi</h1>
      </div>
      <button class="btn btn-primary" onclick="openNewTopicModal()">➕ Buat Topik</button>
    </div>
    
    <div class="flex gap-2 mb-6" style="flex-wrap:wrap">
      <button class="menu-tab active" onclick="filterForum(this,'all')">Semua</button>
      <button class="menu-tab" onclick="filterForum(this,'diet')">💪 Tips Diet</button>
      <button class="menu-tab" onclick="filterForum(this,'resep')">🍳 Resep Sehat</button>
      <button class="menu-tab" onclick="filterForum(this,'motivasi')">🌟 Motivasi</button>
    </div>
    
    <div class="forum-list" id="forumList"></div>
  </div>
</div>

<!-- DONASI PAGE -->
<div id="page-donasi" class="page">
  <div class="container" style="padding-top:32px;padding-bottom:60px">
    <div class="donasi-hero">
      <div style="font-size:3rem;margin-bottom:12px">💝</div>
      <h2>Sebarkan Berkah Bersama KaloriBerkah</h2>
      <p>Setiap kalori yang Anda hitung adalah langkah menuju kesehatan. Setiap donasi yang Anda berikan adalah berkah untuk mereka yang membutuhkan.</p>
      <div class="donasi-counter">
        <div>
          <div class="donasi-counter-num">Rp 125.000.000</div>
          <div class="donasi-counter-label">Total donasi terkumpul</div>
        </div>
      </div>
      <button class="btn btn-orange btn-lg" onclick="openDonasiModal()">🌟 Donasi Sekarang</button>
    </div>

    <div style="display:grid;grid-template-columns:1fr 1fr;gap:28px" class="mt-6">
      <div class="card">
        <h3 style="font-weight:700;margin-bottom:16px">💰 Riwayat Donasi Saya</h3>
        <div id="myDonations">
          <div class="text-center" style="padding:24px;color:var(--text-muted)">
            <div style="font-size:2rem;margin-bottom:8px">📋</div>
            <p class="text-sm">Belum ada donasi. Jadilah yang pertama!</p>
          </div>
        </div>
      </div>
      <div class="card">
        <h3 style="font-weight:700;margin-bottom:16px">👥 Donatur Terbaru</h3>
        <div class="donatur-list" id="donaturList"></div>
      </div>
    </div>
  </div>
</div>

<!-- SETTINGS PAGE -->
<div id="page-settings" class="page">
  <div class="container" style="padding-top:32px;padding-bottom:60px">
    <div class="section-label">Profil</div>
    <h1 class="section-title">Pengaturan</h1>
    <div class="settings-layout">
      <div class="settings-nav">
        <a href="#" class="active" onclick="showSettingsTab('profil',this)">👤 Profil</a>
        <a href="#" onclick="showSettingsTab('target',this)">🎯 Target Kalori</a>
        <a href="#" onclick="showSettingsTab('notif',this)">🔔 Notifikasi</a>
        <a href="#" onclick="showSettingsTab('privasi',this)">🔒 Privasi</a>
        <a href="#" onclick="showSettingsTab('tentang',this)">ℹ️ Tentang</a>
      </div>
      <div>
        <div id="settings-profil">
          <div class="card">
            <h3 style="font-weight:700;margin-bottom:20px">Data Profil</h3>
            <div class="form-group"><label>Nama</label><input type="text" id="sName" placeholder="Nama Anda"></div>
            <div class="form-row">
              <div class="form-group"><label>Usia</label><input type="number" id="sAge" placeholder="25"></div>
              <div class="form-group"><label>Jenis Kelamin</label>
                <select id="sGender"><option value="male">Laki-laki</option><option value="female">Perempuan</option></select>
              </div>
            </div>
            <div class="form-row">
              <div class="form-group"><label>Berat (kg)</label><input type="number" id="sWeight" placeholder="65"></div>
              <div class="form-group"><label>Tinggi (cm)</label><input type="number" id="sHeight" placeholder="170"></div>
            </div>
            <div class="form-group">
              <label>Preferensi Diet</label>
              <select id="sDiet">
                <option value="none">Tidak Ada</option>
                <option value="vegetarian">Vegetarian</option>
                <option value="vegan">Vegan</option>
                <option value="keto">Keto</option>
                <option value="halal">Halal</option>
              </select>
            </div>
            <button class="btn btn-primary" onclick="saveSettings()">💾 Simpan Perubahan</button>
          </div>
        </div>
        <div id="settings-target" class="hidden">
          <div class="card">
            <h3 style="font-weight:700;margin-bottom:20px">Target Kalori Custom</h3>
            <div class="form-group"><label>Target Kalori Harian (kcal)</label><input type="number" id="sTargetKcal" placeholder="1800"></div>
            <div class="form-group"><label>Target Air Minum (gelas)</label><input type="number" id="sTargetWater" placeholder="8"></div>
            <button class="btn btn-primary" onclick="saveTargetSettings()">💾 Simpan Target</button>
          </div>
        </div>
        <div id="settings-notif" class="hidden">
          <div class="card">
            <h3 style="font-weight:700;margin-bottom:20px">Pengaturan Notifikasi</h3>
            <div style="display:flex;flex-direction:column;gap:16px">
              <label style="display:flex;align-items:center;gap:12px;cursor:pointer">
                <input type="checkbox" id="notifSarapan" checked style="width:18px;height:18px">
                <div><div style="font-weight:600">Pengingat Sarapan (07:00)</div><div class="text-xs text-muted">Ingatkan saat waktu sarapan</div></div>
              </label>
              <label style="display:flex;align-items:center;gap:12px;cursor:pointer">
                <input type="checkbox" id="notifMakan" checked style="width:18px;height:18px">
                <div><div style="font-weight:600">Pengingat Makan Siang (12:00)</div><div class="text-xs text-muted">Ingatkan saat waktu makan siang</div></div>
              </label>
              <label style="display:flex;align-items:center;gap:12px;cursor:pointer">
                <input type="checkbox" id="notifAir" checked style="width:18px;height:18px">
                <div><div style="font-weight:600">Pengingat Minum Air</div><div class="text-xs text-muted">Ingatkan setiap 2 jam untuk minum air</div></div>
              </label>
            </div>
            <button class="btn btn-primary mt-4" onclick="showToast('Pengaturan notifikasi disimpan!','success')">💾 Simpan</button>
          </div>
        </div>
        <div id="settings-privasi" class="hidden">
          <div class="card">
            <h3 style="font-weight:700;margin-bottom:20px">Privasi & Data</h3>
            <p class="text-sm text-muted mb-4">Data Anda disimpan secara lokal di perangkat Anda dan tidak dikirim ke server manapun.</p>
            <div style="display:flex;flex-direction:column;gap:12px">
              <button class="btn btn-outline" onclick="exportDataUser()">📥 Download Semua Data Saya</button>
              <button class="btn btn-danger" onclick="if(confirm('Hapus semua data? Tidak bisa dikembalikan!')){clearAllData()}">🗑️ Hapus Semua Data</button>
            </div>
          </div>
        </div>
        <div id="settings-tentang" class="hidden">
          <div class="card">
            <div class="text-center" style="padding:24px">
              <div style="font-size:3rem;margin-bottom:12px">🥗</div>
              <h2 style="font-family:'Sora',sans-serif;font-weight:800;margin-bottom:8px">KaloriBerkah</h2>
              <p class="text-muted text-sm mb-6">Hitung Kalori, Sehatkan Tubuh, Berkahi Hidup</p>
              <p class="text-sm" style="line-height:1.7;color:var(--text-muted)">KaloriBerkah adalah platform kesehatan digital yang menggabungkan kalkulator kalori ilmiah dengan database makanan Indonesia yang lengkap, serta fitur donasi berkah yang terintegrasi.</p>
              <div class="divider"></div>
              <p class="text-xs text-muted">Versi 1.0.0 • © 2024 KaloriBerkah</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ADMIN LOGIN -->
<div id="page-adminLogin" class="page">
  <div class="login-page">
    <div class="login-card">
      <div style="text-align:center;margin-bottom:24px;font-size:2.5rem">🔐</div>
      <h2>Admin KaloriBerkah</h2>
      <p>Masuk ke panel administrasi</p>
      <div class="form-group"><label>Username</label><input type="text" id="adminUser" placeholder="admin" value="admin"></div>
      <div class="form-group"><label>Password</label><input type="password" id="adminPass" placeholder="••••••••" value="admin123" onkeypress="if(event.key==='Enter')adminLogin()"></div>
      <button class="btn btn-primary w-full btn-lg" onclick="adminLogin()">🔐 Masuk</button>
      <div class="text-center mt-4"><a href="#" onclick="showPage('home')" class="text-sm text-muted">← Kembali ke Website</a></div>
    </div>
  </div>
</div>

<!-- ADMIN PANEL -->
<div id="page-admin" class="page">
  <div class="admin-layout">
    <aside class="admin-sidebar">
      <div class="admin-logo">
        <div class="logo">
          <div class="logo-icon">🥗</div>
          <div class="logo-text">Kalori<span style="color:var(--green)">Berkah</span></div>
        </div>
        <div style="font-size:.75rem;color:#94A3B8;margin-top:4px">Panel Admin</div>
      </div>
      <nav class="admin-nav">
        <a href="#" onclick="showAdminSection('dashboard')" class="active"><span>📊</span> Dashboard</a>
        <a href="#" onclick="showAdminSection('foods')"><span>🥘</span> Database Makanan</a>
        <a href="#" onclick="showAdminSection('menus')"><span>🍽️</span> Menu Rekomendasi</a>
        <a href="#" onclick="showAdminSection('donasi')"><span>💝</span> Kelola Donasi</a>
        <a href="#" onclick="showAdminSection('konten')"><span>📝</span> Konten Website</a>
        <a href="#" onclick="showAdminSection('badge')"><span>🏆</span> Badge & Reward</a>
        <div style="flex:1"></div>
        <a href="#" onclick="showPage('home')"><span>↩️</span> Kembali ke Website</a>
        <a href="#" onclick="adminLogout()"><span>🚪</span> Logout</a>
      </nav>
    </aside>
    <main class="admin-main">
      <!-- DASHBOARD -->
      <div id="admin-dashboard">
        <div class="admin-header">
          <h1>📊 Dashboard</h1>
          <div class="text-sm text-muted" id="adminDate"></div>
        </div>
        <div class="stats-grid">
          <div class="stat-card">
            <div class="stat-card-icon">👤</div>
            <div class="stat-card-val">247</div>
            <div class="stat-card-label">User Aktif Hari Ini</div>
          </div>
          <div class="stat-card">
            <div class="stat-card-icon">🧮</div>
            <div class="stat-card-val" id="adminTotalCalc">0</div>
            <div class="stat-card-label">Total Kalori Dihitung</div>
          </div>
          <div class="stat-card">
            <div class="stat-card-icon">💝</div>
            <div class="stat-card-val">Rp 125Jt</div>
            <div class="stat-card-label">Total Donasi</div>
          </div>
          <div class="stat-card">
            <div class="stat-card-icon">🥘</div>
            <div class="stat-card-val" id="adminFoodCount">0</div>
            <div class="stat-card-label">Item Database</div>
          </div>
        </div>
        <div class="card">
          <h3 style="font-weight:700;margin-bottom:16px">📈 Grafik Kalori Rata-rata</h3>
          <div class="chart-wrapper"><canvas id="adminChart"></canvas></div>
        </div>
      </div>

      <!-- FOODS ADMIN -->
      <div id="admin-foods" class="hidden">
        <div class="admin-header">
          <h1>🥘 Database Makanan</h1>
          <button class="btn btn-primary btn-sm" onclick="openAddFoodModal()">➕ Tambah Makanan</button>
        </div>
        <div class="card">
          <div class="flex gap-2 mb-4">
            <input type="text" id="adminFoodSearch" placeholder="🔍 Cari makanan..." oninput="renderAdminFoodTable()" style="flex:1;padding:10px 14px;border:2px solid var(--border);border-radius:8px;font-family:inherit;font-size:.875rem">
          </div>
          <div style="overflow-x:auto">
            <table class="admin-table">
              <thead><tr><th>#</th><th>Nama</th><th>Kalori/100g</th><th>Protein</th><th>Karbo</th><th>Lemak</th><th>Kategori</th><th>Aksi</th></tr></thead>
              <tbody id="adminFoodTable"></tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- MENUS ADMIN -->
      <div id="admin-menus" class="hidden">
        <div class="admin-header"><h1>🍽️ Menu Rekomendasi</h1></div>
        <div id="adminMenuContent"></div>
      </div>

      <!-- DONASI ADMIN -->
      <div id="admin-donasi" class="hidden">
        <div class="admin-header"><h1>💝 Kelola Donasi</h1></div>
        <div class="card mb-4">
          <h3 style="font-weight:700;margin-bottom:16px">🔗 Link Donasi</h3>
          <div class="form-group">
            <label>URL Link Donasi</label>
            <input type="url" id="donasiLink" placeholder="https://linkdonasi.com/kaloriberkah" style="font-size:.875rem">
          </div>
          <button class="btn btn-primary btn-sm" onclick="saveDonasiLink()">💾 Simpan Link</button>
        </div>
        <div class="card">
          <h3 style="font-weight:700;margin-bottom:16px">📋 Riwayat Donasi</h3>
          <table class="admin-table">
            <thead><tr><th>Nama</th><th>Nominal</th><th>Waktu</th><th>Status</th></tr></thead>
            <tbody id="adminDonasiTable"></tbody>
          </table>
        </div>
      </div>

      <!-- KONTEN ADMIN -->
      <div id="admin-konten" class="hidden">
        <div class="admin-header"><h1>📝 Kelola Konten</h1></div>
        <div class="card">
          <h3 style="font-weight:700;margin-bottom:16px">Statistik Hero Section</h3>
          <div class="form-row">
            <div class="form-group"><label>Kalori Dihitung</label><input type="text" id="statCalcInput" placeholder="50.000+"></div>
            <div class="form-group"><label>Total Donasi</label><input type="text" id="statDonasiInput" placeholder="Rp 125Jt+"></div>
          </div>
          <button class="btn btn-primary btn-sm" onclick="saveHeroStats()">💾 Update Statistik</button>
        </div>
      </div>

      <!-- BADGE ADMIN -->
      <div id="admin-badge" class="hidden">
        <div class="admin-header"><h1>🏆 Badge & Reward</h1></div>
        <div class="badge-grid" id="adminBadgeGrid"></div>
      </div>
    </main>
  </div>
</div>

<!-- ===== MODALS ===== -->

<!-- DONASI MODAL -->
<div class="modal-overlay" id="donasiModal">
  <div class="modal">
    <div class="modal-header">
      <div>
        <div style="font-size:1.5rem;margin-bottom:4px">💝</div>
        <div class="modal-title">Donasi Berkah KaloriBerkah</div>
        <div style="font-size:.8rem;color:var(--text-muted);margin-top:4px">Sehatkan tubuh, berkahi hidup</div>
      </div>
      <button class="modal-close" onclick="closeModal('donasiModal')">✕</button>
    </div>
    <div class="modal-body">
      <div style="background:var(--green-light);border-radius:10px;padding:14px 16px;margin-bottom:20px;font-size:.875rem;color:var(--green-dark);line-height:1.6;font-style:italic">
        "Setiap kalori yang Anda hitung adalah langkah menuju kesehatan. Setiap donasi yang Anda berikan adalah berkah untuk mereka yang membutuhkan. Sehatkan tubuh, berkahi hidup."
      </div>
      <div style="font-size:.875rem;font-weight:600;margin-bottom:10px">Pilih Nominal:</div>
      <div class="nominal-grid" id="nominalGrid">
        <button class="nominal-btn" onclick="selectNominal(this,10000)">Rp 10.000</button>
        <button class="nominal-btn" onclick="selectNominal(this,25000)">Rp 25.000</button>
        <button class="nominal-btn" onclick="selectNominal(this,50000)">Rp 50.000</button>
        <button class="nominal-btn" onclick="selectNominal(this,100000)">Rp 100.000</button>
      </div>
      <div class="form-group mt-4">
        <label>Nominal Lain (Rp)</label>
        <input type="number" id="customNominal" placeholder="Masukkan nominal..." oninput="clearNominalSelection()">
      </div>
      <div class="form-group">
        <label>Nama (opsional)</label>
        <input type="text" id="donaturName" placeholder="Nama Anda">
      </div>
      <label style="display:flex;align-items:center;gap:10px;cursor:pointer;font-size:.875rem;margin-bottom:16px">
        <input type="checkbox" id="donasiAnon" style="width:16px;height:16px">
        Saya ingin donasi anonim
      </label>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('donasiModal')">Batal</button>
      <button class="btn btn-orange" onclick="submitDonasi()">🌟 Donasi Sekarang →</button>
    </div>
  </div>
</div>

<!-- DONASI SUCCESS MODAL -->
<div class="modal-overlay" id="donasiSuccessModal">
  <div class="modal">
    <div class="modal-body text-center" style="padding:40px 28px">
      <div style="font-size:4rem;margin-bottom:16px">🎉</div>
      <h2 style="font-family:'Sora',sans-serif;font-weight:800;margin-bottom:8px">Terima Kasih!</h2>
      <p style="color:var(--text-muted);margin-bottom:4px">Semoga menjadi berkah yang berlipat ganda.</p>
      <p style="font-weight:600;color:var(--green);font-size:1.1rem;margin-bottom:24px" id="successNominal"></p>
      <div style="display:flex;flex-direction:column;gap:10px">
        <button class="btn btn-primary" onclick="generateDonasiCertificate()">📄 Download Sertifikat Digital</button>
        <button class="btn btn-outline" onclick="shareWhatsApp()">📱 Bagikan ke WhatsApp</button>
        <button class="btn" style="background:var(--bg);color:var(--text-muted)" onclick="closeModal('donasiSuccessModal')">Tutup</button>
      </div>
    </div>
  </div>
</div>

<!-- ADD FOOD MODAL (ADMIN) -->
<div class="modal-overlay" id="addFoodModal">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="foodModalTitle">➕ Tambah Makanan</div>
      <button class="modal-close" onclick="closeModal('addFoodModal')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-group"><label>Nama Makanan *</label><input type="text" id="af_name" placeholder="Nasi goreng"></div>
      <div class="form-row">
        <div class="form-group"><label>Kalori (per 100g/porsi) *</label><input type="number" id="af_kcal" placeholder="180"></div>
        <div class="form-group"><label>Satuan</label><select id="af_unit"><option value="100g">per 100g</option><option value="porsi">per porsi</option><option value="pcs">per pcs</option></select></div>
      </div>
      <div class="form-row">
        <div class="form-group"><label>Protein (g)</label><input type="number" id="af_protein" placeholder="5"></div>
        <div class="form-group"><label>Karbohidrat (g)</label><input type="number" id="af_karbo" placeholder="30"></div>
      </div>
      <div class="form-row">
        <div class="form-group"><label>Lemak (g)</label><input type="number" id="af_lemak" placeholder="8"></div>
        <div class="form-group"><label>Kategori</label>
          <select id="af_cat"><option value="makanan-indonesia">🇮🇩 Makanan Indonesia</option><option value="makanan-internasional">🌍 Internasional</option><option value="minuman">☕ Minuman</option><option value="snack">🍪 Snack</option></select>
        </div>
      </div>
      <div class="form-group"><label>Emoji/Icon</label><input type="text" id="af_emoji" placeholder="🍽️"></div>
      <div class="form-group"><label>Tag</label>
        <div style="display:flex;gap:12px;flex-wrap:wrap;margin-top:8px">
          <label style="display:flex;align-items:center;gap:6px;font-size:.875rem"><input type="checkbox" id="af_halal"> Halal</label>
          <label style="display:flex;align-items:center;gap:6px;font-size:.875rem"><input type="checkbox" id="af_veg"> Vegetarian</label>
          <label style="display:flex;align-items:center;gap:6px;font-size:.875rem"><input type="checkbox" id="af_gf"> Gluten Free</label>
        </div>
      </div>
      <input type="hidden" id="af_editIndex" value="-1">
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('addFoodModal')">Batal</button>
      <button class="btn btn-primary" onclick="saveFoodItem()">💾 Simpan</button>
    </div>
  </div>
</div>

<!-- NEW TOPIC MODAL -->
<div class="modal-overlay" id="newTopicModal">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">➕ Buat Topik Baru</div>
      <button class="modal-close" onclick="closeModal('newTopicModal')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-group"><label>Nama Anda</label><input type="text" id="topicAuthor" placeholder="Nama pengguna"></div>
      <div class="form-group"><label>Judul Topik *</label><input type="text" id="topicTitle" placeholder="Judul diskusi..."></div>
      <div class="form-group"><label>Kategori</label><select id="topicCat"><option value="diet">💪 Tips Diet</option><option value="resep">🍳 Resep Sehat</option><option value="motivasi">🌟 Motivasi</option></select></div>
      <div class="form-group"><label>Isi Diskusi *</label><textarea id="topicContent" rows="4" placeholder="Tuliskan diskusi Anda..." style="width:100%;padding:11px 16px;border:2px solid var(--border);border-radius:10px;font-family:inherit;font-size:.9rem;resize:vertical"></textarea></div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('newTopicModal')">Batal</button>
      <button class="btn btn-primary" onclick="submitNewTopic()">📤 Posting</button>
    </div>
  </div>
</div>

<!-- MENU DETAIL MODAL -->
<div class="modal-overlay" id="menuDetailModal">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title" id="menuDetailTitle">Detail Menu</div>
      <button class="modal-close" onclick="closeModal('menuDetailModal')">✕</button>
    </div>
    <div class="modal-body" id="menuDetailBody"></div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeModal('menuDetailModal')">Tutup</button>
      <button class="btn btn-primary" onclick="addMenuToLog()">➕ Tambah ke Log</button>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer id="mainFooter">
  <div class="container">
    <div class="footer-grid">
      <div class="footer-brand">
        <div class="logo"><div class="logo-icon">🥗</div><div class="logo-text" style="color:#fff">Kalori<span>Berkah</span></div></div>
        <p>Platform kesehatan digital yang menggabungkan kalkulator kalori ilmiah dengan database makanan Indonesia lengkap dan fitur donasi berkah.</p>
      </div>
      <div class="footer-col">
        <h4>Fitur</h4>
        <a href="#" onclick="scrollToCalc()">Kalkulator Kalori</a>
        <a href="#" onclick="showPage('log')">Log Harian</a>
        <a href="#" onclick="showPage('menu')">Menu Sehat</a>
        <a href="#" onclick="showPage('donasi')">Donasi Berkah</a>
      </div>
      <div class="footer-col">
        <h4>Konten</h4>
        <a href="#" onclick="showPage('blog')">Blog & Artikel</a>
        <a href="#" onclick="showPage('forum')">Forum Komunitas</a>
        <a href="#" onclick="showPage('settings')">Pengaturan</a>
      </div>
      <div class="footer-col">
        <h4>Lainnya</h4>
        <a href="#">Tentang Kami</a>
        <a href="#">Kebijakan Privasi</a>
        <a href="#">FAQ</a>
        <a href="#" onclick="showAdminLogin()">Admin Panel</a>
      </div>
    </div>
    <div class="footer-bottom">
      <span>© 2024 KaloriBerkah — Hitung Kalori, Sehatkan Tubuh, Berkahi Hidup</span>
      <span>Made with 💚 for Indonesia</span>
    </div>
  </div>
</footer>

<script>
// ========== DATABASE MAKANAN ==========
let foodDatabase = [
  // MAKANAN INDONESIA
  {id:1,name:"Nasi Putih",kcal:130,protein:2.7,karbo:28.2,lemak:0.3,unit:"100g",cat:"makanan-indonesia",emoji:"🍚",tags:["halal","vegetarian","gluten-free"]},
  {id:2,name:"Nasi Goreng",kcal:180,protein:4.5,karbo:28,lemak:6.5,unit:"100g",cat:"makanan-indonesia",emoji:"🍳",tags:["halal"]},
  {id:3,name:"Nasi Merah",kcal:111,protein:2.6,karbo:23,lemak:0.9,unit:"100g",cat:"makanan-indonesia",emoji:"🍚",tags:["halal","vegetarian","gluten-free"]},
  {id:4,name:"Soto Ayam",kcal:120,protein:10,karbo:8,lemak:5,unit:"porsi",cat:"makanan-indonesia",emoji:"🍲",tags:["halal"]},
  {id:5,name:"Gado-Gado",kcal:150,protein:8,karbo:15,lemak:7,unit:"porsi",cat:"makanan-indonesia",emoji:"🥗",tags:["halal","vegetarian"]},
  {id:6,name:"Sate Ayam",kcal:180,protein:18,karbo:6,lemak:9,unit:"6 tusuk",cat:"makanan-indonesia",emoji:"🍢",tags:["halal"]},
  {id:7,name:"Rendang Sapi",kcal:250,protein:28,karbo:4,lemak:13,unit:"100g",cat:"makanan-indonesia",emoji:"🥩",tags:["halal"]},
  {id:8,name:"Ayam Goreng",kcal:200,protein:22,karbo:5,lemak:10,unit:"100g",cat:"makanan-indonesia",emoji:"🍗",tags:["halal"]},
  {id:9,name:"Ayam Bakar",kcal:170,protein:24,karbo:3,lemak:7,unit:"100g",cat:"makanan-indonesia",emoji:"🍖",tags:["halal"]},
  {id:10,name:"Tempe Goreng",kcal:170,protein:12,karbo:11,lemak:9,unit:"100g",cat:"makanan-indonesia",emoji:"🟤",tags:["halal","vegetarian"]},
  {id:11,name:"Tahu Goreng",kcal:120,protein:9,karbo:4,lemak:7,unit:"100g",cat:"makanan-indonesia",emoji:"🟨",tags:["halal","vegetarian","gluten-free"]},
  {id:12,name:"Tahu Bumbu Racik",kcal:115,protein:9.5,karbo:5,lemak:6,unit:"porsi",cat:"makanan-indonesia",emoji:"🟡",tags:["halal","vegetarian"]},
  {id:13,name:"Mie Goreng",kcal:140,protein:4.5,karbo:22,lemak:4,unit:"100g",cat:"makanan-indonesia",emoji:"🍜",tags:["halal"]},
  {id:14,name:"Bakso",kcal:160,protein:10,karbo:12,lemak:7,unit:"porsi",cat:"makanan-indonesia",emoji:"🍡",tags:["halal"]},
  {id:15,name:"Rawon",kcal:140,protein:12,karbo:7,lemak:7,unit:"porsi",cat:"makanan-indonesia",emoji:"🍲",tags:["halal"]},
  {id:16,name:"Opor Ayam",kcal:210,protein:18,karbo:5,lemak:12,unit:"porsi",cat:"makanan-indonesia",emoji:"🍛",tags:["halal"]},
  {id:17,name:"Pecel Lele",kcal:230,protein:22,karbo:8,lemak:12,unit:"porsi",cat:"makanan-indonesia",emoji:"🐟",tags:["halal"]},
  {id:18,name:"Ikan Goreng",kcal:180,protein:22,karbo:3,lemak:9,unit:"100g",cat:"makanan-indonesia",emoji:"🐠",tags:["halal","gluten-free"]},
  {id:19,name:"Ikan Kukus",kcal:100,protein:22,karbo:0,lemak:2,unit:"100g",cat:"makanan-indonesia",emoji:"🐡",tags:["halal","gluten-free"]},
  {id:20,name:"Sayur Bayam",kcal:25,protein:2.5,karbo:3,lemak:0.5,unit:"100g",cat:"makanan-indonesia",emoji:"🥬",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:21,name:"Sayur Lodeh",kcal:80,protein:3,karbo:8,lemak:4,unit:"porsi",cat:"makanan-indonesia",emoji:"🥗",tags:["halal","vegetarian"]},
  {id:22,name:"Urap Sayur",kcal:90,protein:3,karbo:9,lemak:5,unit:"porsi",cat:"makanan-indonesia",emoji:"🥗",tags:["halal","vegetarian"]},
  {id:23,name:"Nasi Kuning",kcal:145,protein:3,karbo:30,lemak:2,unit:"100g",cat:"makanan-indonesia",emoji:"🟡",tags:["halal","vegetarian"]},
  {id:24,name:"Ketoprak",kcal:140,protein:7,karbo:18,lemak:5,unit:"porsi",cat:"makanan-indonesia",emoji:"🥗",tags:["halal","vegetarian"]},
  {id:25,name:"Pempek",kcal:160,protein:12,karbo:18,lemak:5,unit:"porsi",cat:"makanan-indonesia",emoji:"🐟",tags:["halal"]},
  {id:26,name:"Martabak Manis",kcal:350,protein:7,karbo:55,lemak:12,unit:"porsi",cat:"makanan-indonesia",emoji:"🥞",tags:["halal"]},
  {id:27,name:"Martabak Asin",kcal:300,protein:14,karbo:28,lemak:16,unit:"porsi",cat:"makanan-indonesia",emoji:"🫓",tags:["halal"]},
  {id:28,name:"Bubur Ayam",kcal:130,protein:9,karbo:18,lemak:3,unit:"porsi",cat:"makanan-indonesia",emoji:"🍚",tags:["halal"]},
  {id:29,name:"Lontong",kcal:110,protein:2,karbo:24,lemak:0.5,unit:"100g",cat:"makanan-indonesia",emoji:"🧊",tags:["halal","vegetarian","gluten-free"]},
  {id:30,name:"Telur Rebus",kcal:80,protein:6,karbo:0.5,lemak:5,unit:"pcs",cat:"makanan-indonesia",emoji:"🥚",tags:["halal","vegetarian","gluten-free"]},
  {id:31,name:"Telur Ceplok",kcal:90,protein:6,karbo:0.5,lemak:7,unit:"pcs",cat:"makanan-indonesia",emoji:"🍳",tags:["halal","vegetarian","gluten-free"]},
  {id:32,name:"Omelet Sayur",kcal:120,protein:8,karbo:4,lemak:8,unit:"pcs",cat:"makanan-indonesia",emoji:"🍳",tags:["halal","vegetarian"]},
  {id:33,name:"Kentang Goreng",kcal:150,protein:2,karbo:20,lemak:7,unit:"100g",cat:"makanan-indonesia",emoji:"🍟",tags:["halal","vegetarian","gluten-free"]},
  {id:34,name:"Pisang Goreng",kcal:130,protein:1.5,karbo:22,lemak:5,unit:"pcs",cat:"makanan-indonesia",emoji:"🍌",tags:["halal","vegetarian"]},
  {id:35,name:"Roti Gandum",kcal:70,protein:3.5,karbo:12,lemak:1,unit:"pcs",cat:"makanan-indonesia",emoji:"🍞",tags:["halal","vegetarian"]},
  // MAKANAN INTERNASIONAL
  {id:36,name:"Pizza Slice",kcal:250,protein:12,karbo:30,lemak:10,unit:"potong",cat:"makanan-internasional",emoji:"🍕",tags:[]},
  {id:37,name:"Sushi Set",kcal:350,protein:20,karbo:50,lemak:5,unit:"6 pcs",cat:"makanan-internasional",emoji:"🍣",tags:["gluten-free"]},
  {id:38,name:"Pasta Carbonara",kcal:320,protein:14,karbo:38,lemak:13,unit:"porsi",cat:"makanan-internasional",emoji:"🍝",tags:[]},
  {id:39,name:"Burger",kcal:540,protein:28,karbo:45,lemak:28,unit:"pcs",cat:"makanan-internasional",emoji:"🍔",tags:[]},
  {id:40,name:"Salad Caesar",kcal:180,protein:10,karbo:12,lemak:10,unit:"porsi",cat:"makanan-internasional",emoji:"🥗",tags:["vegetarian"]},
  {id:41,name:"Steak Sapi",kcal:280,protein:35,karbo:0,lemak:15,unit:"100g",cat:"makanan-internasional",emoji:"🥩",tags:["gluten-free"]},
  {id:42,name:"Sandwich",kcal:280,protein:14,karbo:34,lemak:10,unit:"pcs",cat:"makanan-internasional",emoji:"🥪",tags:[]},
  {id:43,name:"Salad Buah",kcal:70,protein:1,karbo:17,lemak:0.3,unit:"100g",cat:"makanan-internasional",emoji:"🍓",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:44,name:"Oatmeal",kcal:150,protein:5,karbo:27,lemak:2.5,unit:"porsi",cat:"makanan-internasional",emoji:"🥣",tags:["halal","vegetarian"]},
  {id:45,name:"Yogurt Plain",kcal:60,protein:5,karbo:7,lemak:1.5,unit:"100g",cat:"makanan-internasional",emoji:"🫙",tags:["halal","vegetarian","gluten-free"]},
  {id:46,name:"Yogurt Rendah Lemak",kcal:50,protein:5,karbo:6,lemak:0.5,unit:"100g",cat:"makanan-internasional",emoji:"🫙",tags:["halal","vegetarian","gluten-free"]},
  {id:47,name:"Chicken Salad",kcal:200,protein:25,karbo:8,lemak:8,unit:"porsi",cat:"makanan-internasional",emoji:"🥗",tags:["halal","gluten-free"]},
  // BUAH-BUAHAN
  {id:48,name:"Pisang",kcal:89,protein:1.1,karbo:23,lemak:0.3,unit:"pcs",cat:"buah",emoji:"🍌",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:49,name:"Apel",kcal:52,protein:0.3,karbo:14,lemak:0.2,unit:"pcs",cat:"buah",emoji:"🍎",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:50,name:"Jeruk",kcal:62,protein:1.2,karbo:15,lemak:0.2,unit:"pcs",cat:"buah",emoji:"🍊",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:51,name:"Semangka",kcal:30,protein:0.6,karbo:7.5,lemak:0.2,unit:"100g",cat:"buah",emoji:"🍉",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:52,name:"Pepaya",kcal:43,protein:0.5,karbo:11,lemak:0.3,unit:"100g",cat:"buah",emoji:"🫐",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:53,name:"Manga Harum Manis",kcal:65,protein:0.5,karbo:17,lemak:0.3,unit:"100g",cat:"buah",emoji:"🥭",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:54,name:"Alpukat",kcal:160,protein:2,karbo:9,lemak:15,unit:"100g",cat:"buah",emoji:"🥑",tags:["halal","vegetarian","vegan","gluten-free"]},
  // MINUMAN
  {id:55,name:"Air Mineral",kcal:0,protein:0,karbo:0,lemak:0,unit:"gelas",cat:"minuman",emoji:"💧",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:56,name:"Teh Manis",kcal:70,protein:0,karbo:18,lemak:0,unit:"gelas",cat:"minuman",emoji:"🍵",tags:["halal","vegetarian"]},
  {id:57,name:"Teh Hijau Tanpa Gula",kcal:2,protein:0,karbo:0.5,lemak:0,unit:"gelas",cat:"minuman",emoji:"🍵",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:58,name:"Kopi Hitam",kcal:5,protein:0.3,karbo:1,lemak:0,unit:"gelas",cat:"minuman",emoji:"☕",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:59,name:"Kopi Susu Gula Aren",kcal:150,protein:2.5,karbo:22,lemak:5,unit:"gelas",cat:"minuman",emoji:"☕",tags:["halal","vegetarian"]},
  {id:60,name:"Jus Jeruk",kcal:112,protein:1.7,karbo:26,lemak:0.5,unit:"gelas",cat:"minuman",emoji:"🍊",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:61,name:"Jus Alpukat",kcal:180,protein:2,karbo:15,lemak:12,unit:"gelas",cat:"minuman",emoji:"🥑",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:62,name:"Smoothie Buah",kcal:180,protein:3,karbo:38,lemak:2,unit:"gelas",cat:"minuman",emoji:"🥤",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:63,name:"Smoothie Susu Pisang",kcal:210,protein:6,karbo:35,lemak:5,unit:"gelas",cat:"minuman",emoji:"🥤",tags:["halal","vegetarian","gluten-free"]},
  {id:64,name:"Susu Full Cream",kcal:61,protein:3.2,karbo:4.8,lemak:3.3,unit:"100ml",cat:"minuman",emoji:"🥛",tags:["halal","vegetarian","gluten-free"]},
  {id:65,name:"Teh Susu",kcal:90,protein:2,karbo:14,lemak:2.5,unit:"gelas",cat:"minuman",emoji:"🍵",tags:["halal","vegetarian"]},
  {id:66,name:"Es Teh Manis",kcal:80,protein:0,karbo:20,lemak:0,unit:"gelas",cat:"minuman",emoji:"🧊",tags:["halal","vegetarian"]},
  {id:67,name:"Wedang Jahe",kcal:45,protein:0,karbo:11,lemak:0,unit:"gelas",cat:"minuman",emoji:"🫚",tags:["halal","vegetarian","vegan"]},
  // SNACK
  {id:68,name:"Kerupuk",kcal:50,protein:1,karbo:8,lemak:1.5,unit:"5 pcs",cat:"snack",emoji:"🟡",tags:["halal"]},
  {id:69,name:"Cireng",kcal:80,protein:1.5,karbo:14,lemak:2,unit:"2 pcs",cat:"snack",emoji:"⚪",tags:["halal","vegetarian"]},
  {id:70,name:"Cookies Cokelat",kcal:120,protein:1.5,karbo:16,lemak:6,unit:"pcs",cat:"snack",emoji:"🍪",tags:["halal"]},
  {id:71,name:"Cokelat Batangan",kcal:230,protein:3,karbo:28,lemak:12,unit:"pcs",cat:"snack",emoji:"🍫",tags:["halal","vegetarian"]},
  {id:72,name:"Kacang Rebus",kcal:100,protein:5,karbo:8,lemak:5,unit:"porsi",cat:"snack",emoji:"🥜",tags:["halal","vegetarian","vegan","gluten-free"]},
  {id:73,name:"Roti Tawar",kcal:80,protein:3,karbo:15,lemak:1,unit:"pcs",cat:"snack",emoji:"🍞",tags:["halal","vegetarian"]},
  {id:74,name:"Selai Kacang",kcal:100,protein:4,karbo:3,lemak:8,unit:"sdm",cat:"snack",emoji:"🥜",tags:["halal","vegetarian"]},
  {id:75,name:"Granola Bar",kcal:130,protein:3,karbo:20,lemak:5,unit:"pcs",cat:"snack",emoji:"🧁",tags:["halal","vegetarian"]},
  {id:76,name:"Chips Singkong",kcal:90,protein:1,karbo:14,lemak:3,unit:"20g",cat:"snack",emoji:"🟤",tags:["halal","vegetarian","gluten-free"]},
  {id:77,name:"Es Krim Vanila",kcal:200,protein:3.5,karbo:28,lemak:9,unit:"scoop",cat:"snack",emoji:"🍦",tags:["halal","vegetarian"]},
  // MORE INDONESIA
  {id:78,name:"Pepes Ikan",kcal:130,protein:22,karbo:2,lemak:4,unit:"porsi",cat:"makanan-indonesia",emoji:"🐟",tags:["halal","gluten-free"]},
  {id:79,name:"Sayur Asam",kcal:50,protein:2,karbo:8,lemak:1,unit:"porsi",cat:"makanan-indonesia",emoji:"🥣",tags:["halal","vegetarian","vegan"]},
  {id:80,name:"Ikan Bakar",kcal:120,protein:22,karbo:0,lemak:4,unit:"100g",cat:"makanan-indonesia",emoji:"🐟",tags:["halal","gluten-free"]},
  {id:81,name:"Mie Rebus",kcal:110,protein:4,karbo:20,lemak:2,unit:"100g",cat:"makanan-indonesia",emoji:"🍜",tags:["halal"]},
  {id:82,name:"Sop Buntut",kcal:280,protein:25,karbo:6,lemak:16,unit:"porsi",cat:"makanan-indonesia",emoji:"🍲",tags:["halal"]},
  {id:83,name:"Nasi Padang",kcal:350,protein:18,karbo:45,lemak:12,unit:"porsi",cat:"makanan-indonesia",emoji:"🍛",tags:["halal"]},
  {id:84,name:"Tongseng Kambing",kcal:240,protein:22,karbo:8,lemak:14,unit:"porsi",cat:"makanan-indonesia",emoji:"🍲",tags:["halal"]},
  {id:85,name:"Gudeg",kcal:200,protein:6,karbo:28,lemak:8,unit:"porsi",cat:"makanan-indonesia",emoji:"🟤",tags:["halal","vegetarian"]},
  {id:86,name:"Coto Makassar",kcal:250,protein:22,karbo:12,lemak:13,unit:"porsi",cat:"makanan-indonesia",emoji:"🍲",tags:["halal"]},
  {id:87,name:"Laksa",kcal:220,protein:12,karbo:26,lemak:8,unit:"porsi",cat:"makanan-indonesia",emoji:"🍜",tags:["halal"]},
  {id:88,name:"Nasi Liwet",kcal:180,protein:4,karbo:35,lemak:4,unit:"porsi",cat:"makanan-indonesia",emoji:"🍚",tags:["halal"]},
  {id:89,name:"Sate Lilit",kcal:160,protein:15,karbo:5,lemak:9,unit:"porsi",cat:"makanan-indonesia",emoji:"🍢",tags:["halal"]},
  {id:90,name:"Bebek Goreng",kcal:280,protein:26,karbo:3,lemak:18,unit:"100g",cat:"makanan-indonesia",emoji:"🦆",tags:["halal","gluten-free"]},
  // PROTEIN FOODS
  {id:91,name:"Dada Ayam Rebus",kcal:110,protein:24,karbo:0,lemak:2,unit:"100g",cat:"makanan-indonesia",emoji:"🍗",tags:["halal","gluten-free"]},
  {id:92,name:"Tuna Kaleng",kcal:120,protein:25,karbo:0,lemak:3,unit:"100g",cat:"makanan-internasional",emoji:"🐟",tags:["halal","gluten-free"]},
  {id:93,name:"Salmon Panggang",kcal:180,protein:25,karbo:0,lemak:9,unit:"100g",cat:"makanan-internasional",emoji:"🐟",tags:["gluten-free"]},
  {id:94,name:"Telur Dadar",kcal:150,protein:10,karbo:1,lemak:12,unit:"pcs",cat:"makanan-indonesia",emoji:"🍳",tags:["halal","vegetarian","gluten-free"]},
  {id:95,name:"Sosis Sapi",kcal:290,protein:12,karbo:8,lemak:24,unit:"100g",cat:"makanan-indonesia",emoji:"🌭",tags:["halal"]},
  // SNACK TAMBAHAN
  {id:96,name:"Tahu Sumedang",kcal:130,protein:10,karbo:6,lemak:8,unit:"porsi",cat:"snack",emoji:"🟡",tags:["halal","vegetarian"]},
  {id:97,name:"Onde-onde",kcal:120,protein:2,karbo:18,lemak:5,unit:"pcs",cat:"snack",emoji:"⚫",tags:["halal","vegetarian"]},
  {id:98,name:"Lemper",kcal:130,protein:4,karbo:22,lemak:3.5,unit:"pcs",cat:"snack",emoji:"🟤",tags:["halal"]},
  {id:99,name:"Kue Putu",kcal:100,protein:2,karbo:20,lemak:2,unit:"pcs",cat:"snack",emoji:"🟢",tags:["halal","vegetarian"]},
  {id:100,name:"Klepon",kcal:90,protein:1.5,karbo:17,lemak:2,unit:"pcs",cat:"snack",emoji:"🟢",tags:["halal","vegetarian"]},
  {id:101,name:"Madu",kcal:64,protein:0.1,karbo:17,lemak:0,unit:"sdm",cat:"snack",emoji:"🍯",tags:["halal","vegetarian","gluten-free"]},
  {id:102,name:"Keripik Tempe",kcal:120,protein:8,karbo:10,lemak:6,unit:"30g",cat:"snack",emoji:"🟤",tags:["halal","vegetarian"]},
];

// ========== APP STATE ==========
let appState = {
  targetKcal: parseInt(localStorage.getItem('targetKcal')) || 1800,
  targetWater: parseInt(localStorage.getItem('targetWater')) || 8,
  todayLog: JSON.parse(localStorage.getItem('todayLog') || '[]'),
  waterCount: parseInt(localStorage.getItem('waterCount') || '0'),
  weeklyData: JSON.parse(localStorage.getItem('weeklyData') || '[]'),
  userProfile: JSON.parse(localStorage.getItem('userProfile') || '{}'),
  points: parseInt(localStorage.getItem('points') || '0'),
  badges: JSON.parse(localStorage.getItem('badges') || '["pemula"]'),
  donations: JSON.parse(localStorage.getItem('donations') || '[]'),
  donasiLink: localStorage.getItem('donasiLink') || 'https://saweria.co/kaloriberkah',
  currentDonation: 0,
  selectedFood: null,
  currentMenuPaket: null,
  forumTopics: JSON.parse(localStorage.getItem('forumTopics') || '[]'),
  adminLoggedIn: false,
};

// Check date reset
const today = new Date().toDateString();
const lastDate = localStorage.getItem('lastLogDate');
if (lastDate !== today) {
  // Save yesterday to weekly data
  const todayTotal = (JSON.parse(localStorage.getItem('todayLog')||'[]')).reduce((s,f)=>s+f.kcal,0);
  let weekly = JSON.parse(localStorage.getItem('weeklyData')||'[]');
  weekly.push({date: lastDate || today, kcal: todayTotal});
  if(weekly.length > 7) weekly = weekly.slice(-7);
  localStorage.setItem('weeklyData', JSON.stringify(weekly));
  appState.weeklyData = weekly;
  localStorage.setItem('lastLogDate','');
  localStorage.setItem('todayLog','[]');
  localStorage.setItem('waterCount','0');
  appState.todayLog = [];
  appState.waterCount = 0;
  localStorage.setItem('lastLogDate', today);
}

// ========== NAVIGATION ==========
function showPage(id) {
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  document.querySelectorAll('.nav-links a').forEach(a=>a.classList.remove('active'));
  const navEl = document.getElementById('nav-'+id);
  if(navEl) navEl.classList.add('active');
  const isAdmin = ['admin','adminLogin'].includes(id);
  document.getElementById('mainNav').style.display = isAdmin ? 'none' : '';
  document.getElementById('mainFooter').style.display = isAdmin ? 'none' : '';
  window.scrollTo(0,0);
  if(id==='log') initLogPage();
  if(id==='menu') renderMenuPage('rendah');
  if(id==='blog') renderBlogGrid();
  if(id==='forum') renderForum('all');
  if(id==='donasi') renderDonasiPage();
  if(id==='settings') loadSettingsData();
  if(id==='admin') initAdmin();
}

function toggleMobileMenu() {
  const m = document.getElementById('mobileMenu');
  m.classList.toggle('hidden');
}

function showAdminLogin() { showPage('adminLogin'); }

// ========== CALCULATOR ==========
function calculateCalories() {
  const age = parseFloat(document.getElementById('calcAge').value);
  const gender = document.getElementById('calcGender').value;
  const weight = parseFloat(document.getElementById('calcWeight').value);
  const height = parseFloat(document.getElementById('calcHeight').value);
  const activity = parseFloat(document.getElementById('calcActivity').value);
  const goal = document.getElementById('calcGoal').value;
  const name = document.getElementById('calcName').value;
  if(!age||!gender||!weight||!height||!activity||!goal) {
    showToast('Mohon lengkapi semua field yang wajib diisi!','error'); return;
  }
  const s = gender==='male' ? 5 : -161;
  const bmr = (10*weight) + (6.25*height) - (5*age) + s;
  const tdee = bmr * activity;
  let target = tdee;
  let goalText = '';
  if(goal==='lose'){target=tdee-500;goalText='Turun berat badan (-500 kcal/hari)'}
  else if(goal==='gain'){target=tdee+500;goalText='Naik berat badan (+500 kcal/hari)'}
  else goalText='Mempertahankan berat badan';
  const protein = Math.round((target*0.25)/4);
  const karbo = Math.round((target*0.50)/4);
  const lemak = Math.round((target*0.25)/9);
  document.getElementById('resultKcal').textContent = Math.round(target).toLocaleString();
  document.getElementById('rProtein').textContent = protein+'g';
  document.getElementById('rKarbo').textContent = karbo+'g';
  document.getElementById('rLemak').textContent = lemak+'g';
  document.getElementById('resultName').textContent = name ? `Halo, ${name}! 👋` : '';
  document.getElementById('resultDetail').innerHTML = `
    BMR: <strong>${Math.round(bmr)} kcal</strong> | TDEE: <strong>${Math.round(tdee)} kcal</strong><br>
    Tujuan: <strong>${goalText}</strong>
  `;
  document.getElementById('resultCard').classList.add('show');
  document.getElementById('calcPlaceholder').style.display='none';
  // Save to state
  appState.targetKcal = Math.round(target);
  appState.userProfile = {name,age,gender,weight,height,activity,goal,protein,karbo,lemak};
  localStorage.setItem('targetKcal', appState.targetKcal);
  localStorage.setItem('userProfile', JSON.stringify(appState.userProfile));
  // Add points
  addPoints(10);
  showToast(`Kebutuhan kalori Anda: ${Math.round(target)} kcal/hari 🎉`,'success');
  // Update log page target
  document.getElementById('progressTarget').textContent = `Target: ${Math.round(target)} kcal`;
  document.getElementById('totalRemaining').textContent = Math.round(target);
}

function scrollToCalc() {
  showPage('home');
  setTimeout(()=>document.getElementById('calcSection').scrollIntoView({behavior:'smooth'}),100);
}

// ========== LOG PAGE ==========
function initLogPage() {
  const d = new Date();
  document.getElementById('logDate').textContent = `📅 ${d.toLocaleDateString('id-ID',{weekday:'long',year:'numeric',month:'long',day:'numeric'})}`;
  document.getElementById('progressTarget').textContent = `Target: ${appState.targetKcal} kcal`;
  renderWaterTracker();
  updateLogProgress();
  renderLogByCategory();
  renderWeeklyChart();
  renderMacroChart();
  updateTips();
  document.getElementById('userPoints').textContent = appState.points + ' Poin';
}

function renderWaterTracker() {
  const c = document.getElementById('waterTracker');
  c.innerHTML = '';
  for(let i=0;i<appState.targetWater;i++){
    const g = document.createElement('div');
    g.className = 'water-glass' + (i<appState.waterCount?' filled':'');
    g.textContent = i<appState.waterCount ? '💧' : '🔲';
    g.onclick = ()=>toggleWater(i);
    c.appendChild(g);
  }
  document.getElementById('waterCount').textContent = `${appState.waterCount} dari ${appState.targetWater} gelas`;
}

function toggleWater(idx) {
  appState.waterCount = idx < appState.waterCount ? idx : idx+1;
  localStorage.setItem('waterCount', appState.waterCount);
  renderWaterTracker();
  if(appState.waterCount===appState.targetWater) showToast('🎉 Target minum air tercapai!','success');
}

function updateLogProgress() {
  const total = appState.todayLog.reduce((s,f)=>s+f.kcal,0);
  const target = appState.targetKcal;
  const pct = Math.min(Math.round((total/target)*100),100);
  const fill = document.getElementById('progressFill');
  fill.style.width = pct+'%';
  fill.className = 'progress-fill' + (pct>100?' danger':pct>85?' warning':'');
  document.getElementById('progressPct').textContent = pct+'%';
  document.getElementById('logProgressText').textContent = `${total.toLocaleString()} / ${target.toLocaleString()} kcal`;
  document.getElementById('totalConsumed').textContent = total.toLocaleString();
  document.getElementById('totalRemaining').textContent = Math.max(0,target-total).toLocaleString();
  const proto = appState.todayLog.reduce((s,f)=>s+(f.protein||0),0);
  const carb = appState.todayLog.reduce((s,f)=>s+(f.karbo||0),0);
  document.getElementById('totalProtein').textContent = Math.round(proto)+'g';
  document.getElementById('totalKarbo').textContent = Math.round(carb)+'g';
  if(total>target*1.1) showToast('⚠️ Kalori harian sudah melebihi target!','warning');
}

function renderLogByCategory() {
  const cats = {sarapan:'🌅 Sarapan',siang:'☀️ Makan Siang',malam:'🌙 Makan Malam',snack:'🍪 Snack',minuman:'☕ Minuman'};
  const container = document.getElementById('logByCategory');
  const empty = document.getElementById('emptyLog');
  if(!appState.todayLog.length){container.innerHTML='';empty.style.display='';return;}
  empty.style.display='none';
  let html = '';
  Object.entries(cats).forEach(([key,label])=>{
    const items = appState.todayLog.filter(f=>f.category===key);
    if(!items.length) return;
    html += `<div class="mb-4"><div style="font-size:.8rem;font-weight:700;color:var(--text-muted);text-transform:uppercase;letter-spacing:.05em;margin-bottom:8px">${label}</div>
      <table class="log-table"><thead><tr><th>Makanan</th><th>Porsi</th><th>Kalori</th><th>Protein</th><th></th></tr></thead><tbody>`;
    items.forEach((f,i)=>{
      html += `<tr><td><strong>${f.emoji||'🍽️'} ${f.name}</strong></td><td class="text-muted">${f.portion}g</td><td class="text-green font-bold">${f.kcal} kcal</td><td class="text-muted">${f.protein||0}g</td><td><button class="del-btn" onclick="removeLogItem('${f.id}')">✕</button></td></tr>`;
    });
    html += `</tbody></table></div>`;
  });
  container.innerHTML = html;
}

let weeklyChartInstance = null, macroChartInstance = null;

function renderWeeklyChart() {
  const ctx = document.getElementById('weeklyChart');
  if(!ctx) return;
  if(weeklyChartInstance) weeklyChartInstance.destroy();
  const labels = [];
  const data = [];
  const days = ['Min','Sen','Sel','Rab','Kam','Jum','Sab'];
  for(let i=6;i>=0;i--){
    const d = new Date(); d.setDate(d.getDate()-i);
    labels.push(days[d.getDay()]);
    const found = appState.weeklyData.find(w=>w.date===d.toDateString());
    data.push(found ? found.kcal : (i===0?appState.todayLog.reduce((s,f)=>s+f.kcal,0):0));
  }
  weeklyChartInstance = new Chart(ctx,{type:'line',data:{labels,datasets:[{label:'Kalori (kcal)',data,borderColor:'#10B981',backgroundColor:'rgba(16,185,129,.1)',borderWidth:2.5,tension:.4,pointBackgroundColor:'#10B981',pointRadius:4,fill:true}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{beginAtZero:true,grid:{color:'rgba(0,0,0,.05)'},ticks:{font:{size:11}}},x:{grid:{display:false},ticks:{font:{size:11}}}}}});
}

function renderMacroChart() {
  const ctx = document.getElementById('macroChart');
  if(!ctx) return;
  if(macroChartInstance) macroChartInstance.destroy();
  const p = appState.todayLog.reduce((s,f)=>s+(f.protein||0),0);
  const k = appState.todayLog.reduce((s,f)=>s+(f.karbo||0),0);
  const l = appState.todayLog.reduce((s,f)=>s+(f.lemak||0),0);
  macroChartInstance = new Chart(ctx,{type:'doughnut',data:{labels:['Protein','Karbohidrat','Lemak'],datasets:[{data:[p||1,k||1,l||1],backgroundColor:['#10B981','#F59E0B','#60A5FA'],borderWidth:0}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'bottom',labels:{font:{size:11},padding:16}}}}});
}

function updateTips() {
  const total = appState.todayLog.reduce((s,f)=>s+f.kcal,0);
  const target = appState.targetKcal;
  const tips = [
    total < target*0.3 ? '💡 Kamu belum banyak makan hari ini. Pastikan asupan kalori cukup untuk energi!' : '',
    total > target ? '⚠️ Kalori sudah melebihi target! Coba pilih makanan rendah kalori untuk waktu makan selanjutnya.' : '',
    total >= target*0.8 && total <= target ? '✅ Bagus! Kamu hampir mencapai target kalori harian.' : '',
    '🥗 Ingat untuk mengonsumsi sayur dan buah setiap hari untuk vitamin dan mineral!',
  ].filter(Boolean);
  const tip = document.getElementById('personalTip');
  if(tip) tip.textContent = tips[Math.floor(Math.random()*tips.length)] || '💡 Catat setiap makanan yang dikonsumsi untuk hasil tracking yang akurat!';
}

// ========== FOOD SEARCH ==========
let debounceTimer;
function searchFood(query) {
  clearTimeout(debounceTimer);
  debounceTimer = setTimeout(()=>{
    const list = document.getElementById('autocompleteList');
    if(!query || query.length < 2) { list.classList.remove('show'); return; }
    const results = foodDatabase.filter(f=>f.name.toLowerCase().includes(query.toLowerCase())).slice(0,8);
    if(!results.length){list.classList.remove('show');return;}
    list.innerHTML = results.map(f=>`
      <div class="ac-item" onclick="selectFood(${f.id})">
        <span>${f.emoji} ${f.name}</span>
        <span class="ac-kcal">${f.kcal} kcal/${f.unit}</span>
      </div>`).join('');
    list.classList.add('show');
  }, 150);
}

function selectFood(id) {
  const f = foodDatabase.find(x=>x.id===id);
  if(!f) return;
  appState.selectedFood = f;
  document.getElementById('foodSearch').value = f.name;
  document.getElementById('foodKcal').value = f.kcal;
  document.getElementById('autocompleteList').classList.remove('show');
  document.getElementById('selectedFoodInfo').classList.remove('hidden');
  document.getElementById('selectedFoodName').textContent = `${f.emoji} ${f.name}`;
  document.getElementById('selectedFoodDetail').textContent = `${f.kcal} kcal/${f.unit} | P:${f.protein}g K:${f.karbo}g L:${f.lemak}g`;
  document.getElementById('foodPortion').value = 100;
  document.getElementById('foodPortion').oninput = function(){
    const ratio = this.value/100;
    document.getElementById('foodKcal').value = Math.round(f.kcal*ratio);
  };
}

function addFoodToLog() {
  const name = document.getElementById('foodSearch').value.trim();
  const kcal = parseFloat(document.getElementById('foodKcal').value);
  const cat = document.getElementById('mealCategory').value;
  const portion = parseFloat(document.getElementById('foodPortion').value) || 100;
  if(!name||!kcal){showToast('Masukkan nama dan kalori makanan!','error');return;}
  const f = appState.selectedFood;
  const ratio = portion/100;
  const item = {
    id: Date.now().toString(),
    name, kcal: Math.round(kcal),
    protein: f ? Math.round(f.protein*ratio*10)/10 : 0,
    karbo: f ? Math.round(f.karbo*ratio*10)/10 : 0,
    lemak: f ? Math.round(f.lemak*ratio*10)/10 : 0,
    portion, category: cat,
    emoji: f ? f.emoji : '🍽️',
    time: new Date().toLocaleTimeString('id-ID',{hour:'2-digit',minute:'2-digit'})
  };
  appState.todayLog.push(item);
  localStorage.setItem('todayLog', JSON.stringify(appState.todayLog));
  localStorage.setItem('lastLogDate', today);
  document.getElementById('foodSearch').value='';
  document.getElementById('foodKcal').value='';
  document.getElementById('foodPortion').value='100';
  document.getElementById('selectedFoodInfo').classList.add('hidden');
  appState.selectedFood = null;
  updateLogProgress();
  renderLogByCategory();
  renderMacroChart();
  addPoints(10);
  showToast(`✅ ${name} (${Math.round(kcal)} kcal) ditambahkan!`,'success');
}

function removeLogItem(id) {
  appState.todayLog = appState.todayLog.filter(f=>f.id!==id);
  localStorage.setItem('todayLog', JSON.stringify(appState.todayLog));
  updateLogProgress();
  renderLogByCategory();
  renderMacroChart();
  showToast('Item dihapus dari log','');
}

function clearTodayLog() {
  if(!confirm('Reset log hari ini?')) return;
  appState.todayLog = [];
  localStorage.setItem('todayLog','[]');
  updateLogProgress();
  renderLogByCategory();
  showToast('Log hari ini direset','');
}

document.addEventListener('click',e=>{
  if(!e.target.closest('#foodSearch')&&!e.target.closest('#autocompleteList')){
    const list=document.getElementById('autocompleteList');
    if(list) list.classList.remove('show');
  }
});

// ========== MENU PAGE ==========
const menuData = {
  rendah: {
    title: '🥗 Paket Rendah Kalori',
    desc: 'Ideal untuk program penurunan berat badan. Target 1.500–1.700 kcal/hari.',
    target: '1.500–1.700 kcal',
    color: '#D1FAE5',
    borderColor: '#10B981',
    items: [
      {meal:'Sarapan',name:'Omelet Sayur + Roti Gandum',kcal:350,emoji:'🍳',time:'10 mnt',protein:18,karbo:30,lemak:12,
       ingredients:['2 butir telur','1 lembar roti gandum','Bayam, wortel, tomat','Garam, merica, minyak zaitun'],
       steps:['Kocok telur, beri garam dan merica','Tumis sayuran sebentar di wajan anti lengket','Masukkan telur, masak hingga matang','Sajikan dengan roti gandum yang sudah dipanggang']},
      {meal:'Snack Pagi',name:'Buah Apel Segar',kcal:80,emoji:'🍎',time:'0 mnt',protein:0.4,karbo:21,lemak:0.2,
       ingredients:['1 buah apel merah/hijau segar'],steps:['Cuci bersih','Kupas atau makan langsung dengan kulitnya']},
      {meal:'Makan Siang',name:'Nasi Merah + Ikan Kukus + Bayam',kcal:450,emoji:'🍚',time:'25 mnt',protein:30,karbo:55,lemak:8,
       ingredients:['100g nasi merah','150g ikan kukus','100g sayur bayam','Bumbu: bawang putih, jahe, garam'],
       steps:['Masak nasi merah seperti biasa','Kukus ikan yang sudah dibumbui 15 menit','Tumis bayam dengan bawang putih','Sajikan lengkap']},
      {meal:'Snack Sore',name:'Yogurt Rendah Lemak',kcal:120,emoji:'🫙',time:'0 mnt',protein:10,karbo:12,lemak:1,
       ingredients:['200g yogurt rendah lemak plain','Buah segar optional'],steps:['Tuang yogurt ke dalam mangkuk','Tambahkan potongan buah segar optional','Nikmati dingin']},
      {meal:'Makan Malam',name:'Salad Ayam Panggang',kcal:350,emoji:'🥗',time:'20 mnt',protein:32,karbo:15,lemak:12,
       ingredients:['150g dada ayam','Selada, timun, tomat, wortel','Dressing: lemon, olive oil, garam'],
       steps:['Panggang ayam yang sudah dibumbui garam-merica','Potong semua sayuran segar','Campurkan sayuran dan ayam','Buat dressing: lemon + olive oil + garam, aduk']},
      {meal:'Minuman',name:'Air Putih 8 Gelas + Teh Hijau',kcal:5,emoji:'💧',time:'0 mnt',protein:0,karbo:1,lemak:0,
       ingredients:['Air putih mineral','Teh hijau tanpa gula'],steps:['Minum air minimal 8 gelas sepanjang hari','Seduh teh hijau tanpa gula pagi dan sore']},
    ]
  },
  seimbang: {
    title: '⚖️ Paket Seimbang',
    desc: 'Untuk mempertahankan berat badan ideal. Target 1.800–2.000 kcal/hari.',
    target: '1.800–2.000 kcal',
    color: '#FEF3C7',
    borderColor: '#F59E0B',
    items: [
      {meal:'Sarapan',name:'Nasi Goreng Sayur + Telur Rebus',kcal:500,emoji:'🍳',time:'15 mnt',protein:18,karbo:65,lemak:14,
       ingredients:['150g nasi putih','2 butir telur','Wortel, kacang polong, bawang','Kecap, garam, minyak goreng'],
       steps:['Goreng bawang putih hingga harum','Masukkan sayuran, tumis sebentar','Masukkan nasi, tambahkan kecap dan garam','Goreng telur atau rebus terpisah']},
      {meal:'Snack Pagi',name:'Pisang Matang',kcal:105,emoji:'🍌',time:'0 mnt',protein:1.3,karbo:27,lemak:0.4,
       ingredients:['1 buah pisang kepok/ambon matang'],steps:['Pilih pisang yang sudah matang sempurna','Kupas dan nikmati langsung']},
      {meal:'Makan Siang',name:'Nasi + Ayam Bakar + Tempe + Sayur',kcal:600,emoji:'🍛',time:'30 mnt',protein:35,karbo:70,lemak:18,
       ingredients:['150g nasi putih','150g ayam bakar bumbu','100g tempe goreng','Sayur tumis campur'],
       steps:['Marinasi ayam dengan bumbu bakar semalam','Panggang ayam diatas bara/teflon','Goreng tempe hingga kecokelatan','Tumis sayur dengan bumbu sederhana']},
      {meal:'Snack Sore',name:'Kacang Rebus',kcal:150,emoji:'🥜',time:'20 mnt',protein:8,karbo:13,lemak:7,
       ingredients:['100g kacang tanah','Garam secukupnya','Air untuk merebus'],
       steps:['Rendam kacang semalaman','Rebus dengan air garam','Masak hingga empuk sekitar 20 menit','Tiriskan dan sajikan hangat']},
      {meal:'Makan Malam',name:'Ikan Goreng + Nasi + Urap Sayur',kcal:500,emoji:'🐟',time:'25 mnt',protein:32,karbo:55,lemak:16,
       ingredients:['150g ikan goreng','100g nasi putih','Urap: kelapa parut, bayam, kacang panjang'],
       steps:['Goreng ikan yang sudah dibumbui hingga keemasan','Masak sayuran untuk urap','Campur sayur dengan kelapa parut bumbu','Sajikan lengkap bersama nasi']},
      {meal:'Minuman',name:'Teh Manis 2 Gelas + Air Putih',kcal:140,emoji:'🍵',time:'5 mnt',protein:0,karbo:36,lemak:0,
       ingredients:['Teh celup 2 kantong','Gula 2 sdt per gelas','Air mineral secukupnya'],
       steps:['Seduh teh di pagi dan sore hari','Minum air putih minimal 6 gelas']},
    ]
  },
  tinggi: {
    title: '💪 Paket Tinggi Kalori',
    desc: 'Untuk program penambahan massa otot dan berat badan. Target 2.200–2.500 kcal/hari.',
    target: '2.200–2.500 kcal',
    color: '#DBEAFE',
    borderColor: '#3B82F6',
    items: [
      {meal:'Sarapan',name:'Nasi + Telur Ceplok + Sosis',kcal:700,emoji:'🍳',time:'20 mnt',protein:28,karbo:80,lemak:26,
       ingredients:['200g nasi putih','2 butir telur ceplok','2 buah sosis sapi','Sambal, kecap manis'],
       steps:['Goreng telur dengan sedikit minyak','Goreng sosis hingga kecokelatan','Sajikan dengan nasi dan sambal','Tambahkan kecap manis sesuai selera']},
      {meal:'Snack Pagi',name:'Roti Tawar + Selai Kacang',kcal:300,emoji:'🍞',time:'5 mnt',protein:12,karbo:32,lemak:16,
       ingredients:['3 lembar roti tawar','3 sdm selai kacang','Madu optional'],
       steps:['Oleskan selai kacang tebal di roti','Tambahkan madu jika suka','Gulung atau makan langsung']},
      {meal:'Makan Siang',name:'Nasi + Rendang + Kentang',kcal:800,emoji:'🥘',time:'45 mnt',protein:40,karbo:90,lemak:28,
       ingredients:['200g nasi putih','150g rendang sapi','100g kentang goreng','Sayur campur'],
       steps:['Hangatkan rendang yang sudah dimasak','Goreng kentang hingga keemasan','Siapkan sayuran rebus','Sajikan semua di piring besar']},
      {meal:'Snack Sore',name:'Smoothie Susu Pisang Madu',kcal:400,emoji:'🥤',time:'5 mnt',protein:10,karbo:68,lemak:8,
       ingredients:['2 buah pisang matang','250ml susu full cream','1 sdm madu','Kayu manis bubuk'],
       steps:['Masukkan semua bahan ke blender','Blend hingga halus dan creamy','Tuang ke gelas, tabur kayu manis','Nikmati dingin']},
      {meal:'Makan Malam',name:'Mie Goreng Ayam + Telur + Bakso',kcal:500,emoji:'🍜',time:'20 mnt',protein:30,karbo:65,lemak:16,
       ingredients:['100g mie kuning','100g ayam goreng','3 butir bakso','1 telur','Bumbu mie goreng'],
       steps:['Rebus mie hingga matang','Tumis bumbu halus hingga harum','Masukkan mie, ayam, bakso','Buat dadar tipis dari telur sebagai topping']},
      {meal:'Minuman',name:'Kopi Susu 2 Gelas + Air Putih',kcal:300,emoji:'☕',time:'5 mnt',protein:5,karbo:44,lemak:10,
       ingredients:['2 sachet kopi susu instan','Susu tambahan optional','Air mineral cukup'],
       steps:['Seduh kopi susu pagi dan sore','Minum air putih minimal 6 gelas sepanjang hari']},
    ]
  }
};

let currentMenuDetail = null;

function renderMenuPage(paket) {
  const data = menuData[paket];
  if(!data) return;
  const totalKcal = data.items.reduce((s,i)=>s+i.kcal,0);
  let html = `
    <div class="card mb-6" style="background:${data.color};border-color:${data.borderColor}">
      <div class="flex items-center justify-between flex-wrap gap-2">
        <div><h2 style="font-family:'Sora',sans-serif;font-weight:800;font-size:1.4rem;margin-bottom:4px">${data.title}</h2>
        <p style="color:var(--text-muted);font-size:.9rem">${data.desc}</p></div>
        <div style="text-align:right">
          <div style="font-family:'Sora',sans-serif;font-size:2rem;font-weight:800;color:${data.borderColor}">${totalKcal.toLocaleString()}</div>
          <div style="font-size:.8rem;color:var(--text-muted)">kcal total • Target: ${data.target}</div>
        </div>
      </div>
    </div>
    <div class="menu-grid">`;
  data.items.forEach((item,i)=>{
    html += `<div class="menu-card">
      <div class="menu-card-img">${item.emoji}</div>
      <div class="menu-card-body">
        <div style="font-size:.75rem;font-weight:700;color:var(--text-muted);text-transform:uppercase;margin-bottom:4px">${item.meal}</div>
        <div class="menu-card-title">${item.name}</div>
        <div class="menu-card-kcal">${item.kcal} kcal</div>
        <div class="flex gap-2 items-center">
          <span class="menu-card-time">⏱️ ${item.time}</span>
          <span class="tag tag-green">Halal</span>
        </div>
        <div style="display:flex;gap:6px;margin-top:12px">
          <button class="btn btn-outline btn-sm" onclick="openMenuDetail(${i},'${paket}')">📖 Resep</button>
          <button class="btn btn-primary btn-sm" onclick="quickAddMenu(${i},'${paket}')">➕ Log</button>
        </div>
      </div>
    </div>`;
  });
  html += '</div>';
  html += `<div class="text-center mt-8">
    <button class="btn btn-outline" onclick="generateShoppingList('${paket}')">🛒 Buat Daftar Belanja</button>
  </div>`;
  document.getElementById('menuContent').innerHTML = html;
}

function switchMenuTab(el, paket) {
  document.querySelectorAll('.menu-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  renderMenuPage(paket);
}

function openMenuDetail(idx, paket) {
  const item = menuData[paket].items[idx];
  currentMenuDetail = {item, paket};
  document.getElementById('menuDetailTitle').textContent = `${item.emoji} ${item.name}`;
  document.getElementById('menuDetailBody').innerHTML = `
    <div style="background:var(--green-light);border-radius:10px;padding:14px;display:grid;grid-template-columns:repeat(4,1fr);gap:8px;text-align:center;margin-bottom:20px">
      <div><div style="font-weight:800;font-size:1.2rem;color:var(--green)">${item.kcal}</div><div style="font-size:.75rem;color:var(--text-muted)">kcal</div></div>
      <div><div style="font-weight:800;font-size:1.2rem">${item.protein}g</div><div style="font-size:.75rem;color:var(--text-muted)">Protein</div></div>
      <div><div style="font-weight:800;font-size:1.2rem">${item.karbo}g</div><div style="font-size:.75rem;color:var(--text-muted)">Karbo</div></div>
      <div><div style="font-weight:800;font-size:1.2rem">${item.lemak}g</div><div style="font-size:.75rem;color:var(--text-muted)">Lemak</div></div>
    </div>
    <div style="font-weight:700;margin-bottom:10px">🛒 Bahan-bahan:</div>
    <ul style="list-style:none;margin-bottom:20px">${item.ingredients.map(b=>`<li style="padding:6px 0;border-bottom:1px solid var(--border);font-size:.875rem">• ${b}</li>`).join('')}</ul>
    <div style="font-weight:700;margin-bottom:10px">👩‍🍳 Cara Memasak:</div>
    <ol style="padding-left:20px">${item.steps.map(s=>`<li style="margin-bottom:8px;font-size:.875rem;line-height:1.6">${s}</li>`).join('')}</ol>`;
  openModal('menuDetailModal');
}

function addMenuToLog() {
  if(!currentMenuDetail) return;
  const {item, paket} = currentMenuDetail;
  const catMap = {Sarapan:'sarapan','Snack Pagi':'snack','Makan Siang':'siang','Snack Sore':'snack','Makan Malam':'malam',Minuman:'minuman'};
  appState.todayLog.push({
    id: Date.now().toString(),
    name: item.name, kcal: item.kcal,
    protein: item.protein, karbo: item.karbo, lemak: item.lemak,
    portion: 1, category: catMap[item.meal]||'siang',
    emoji: item.emoji,
    time: new Date().toLocaleTimeString('id-ID',{hour:'2-digit',minute:'2-digit'})
  });
  localStorage.setItem('todayLog', JSON.stringify(appState.todayLog));
  closeModal('menuDetailModal');
  showToast(`✅ ${item.name} ditambahkan ke log!`,'success');
}

function quickAddMenu(idx, paket) {
  const item = menuData[paket].items[idx];
  const catMap = {Sarapan:'sarapan','Snack Pagi':'snack','Makan Siang':'siang','Snack Sore':'snack','Makan Malam':'malam',Minuman:'minuman'};
  appState.todayLog.push({
    id: Date.now().toString(),
    name: item.name, kcal: item.kcal,
    protein: item.protein, karbo: item.karbo, lemak: item.lemak,
    portion: 1, category: catMap[item.meal]||'siang',
    emoji: item.emoji,
    time: new Date().toLocaleTimeString('id-ID',{hour:'2-digit',minute:'2-digit'})
  });
  localStorage.setItem('todayLog', JSON.stringify(appState.todayLog));
  showToast(`✅ ${item.name} (${item.kcal} kcal) ditambahkan!`,'success');
}

function generateShoppingList(paket) {
  const data = menuData[paket];
  let list = `🛒 *DAFTAR BELANJA - ${data.title}*\n\n`;
  data.items.forEach(item=>{
    list += `*${item.meal}: ${item.name}*\n`;
    item.ingredients.forEach(b=>list+=`  • ${b}\n`);
    list += '\n';
  });
  list += `_Generated dari KaloriBerkah - ${new Date().toLocaleDateString('id-ID')}_`;
  const wa = `https://wa.me/?text=${encodeURIComponent(list)}`;
  window.open(wa,'_blank');
}

// ========== BLOG ==========
const blogPosts = [
  {id:1,title:'Cara Hitung Kalori yang Benar',cat:'Panduan',emoji:'📊',bg:'#D1FAE5',
   content:`<h2 style="font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800;margin-bottom:16px">Cara Hitung Kalori yang Benar</h2>
<p style="color:var(--text-muted);margin-bottom:20px">Diterbitkan 10 Januari 2024 • 5 menit baca</p>
<p style="margin-bottom:16px;line-height:1.8">Menghitung kalori adalah langkah awal yang penting dalam perjalanan hidup sehat. Namun, banyak orang masih bingung tentang cara yang tepat untuk melakukannya.</p>
<h3 style="font-weight:700;margin:20px 0 10px">1. Kenali Konsep BMR</h3>
<p style="margin-bottom:16px;line-height:1.8">BMR (Basal Metabolic Rate) adalah jumlah kalori yang dibutuhkan tubuh untuk menjalankan fungsi dasar seperti bernapas, sirkulasi darah, dan produksi sel. BMR dihitung berdasarkan usia, tinggi badan, berat badan, dan jenis kelamin.</p>
<h3 style="font-weight:700;margin:20px 0 10px">2. Hitung TDEE</h3>
<p style="margin-bottom:16px;line-height:1.8">TDEE (Total Daily Energy Expenditure) adalah total kalori yang dibutuhkan dalam sehari, termasuk aktivitas fisik. Rumus: TDEE = BMR × Faktor Aktivitas. Faktor aktivitas berkisar dari 1.2 (sangat sedentary) hingga 1.9 (sangat aktif).</p>
<h3 style="font-weight:700;margin:20px 0 10px">3. Sesuaikan dengan Tujuan</h3>
<p style="margin-bottom:16px;line-height:1.8">Untuk menurunkan berat badan, kurangi 500 kcal/hari dari TDEE. Untuk menaikkan, tambah 300-500 kcal. Jangan kurangi terlalu drastis karena bisa memperlambat metabolisme.</p>
<h3 style="font-weight:700;margin:20px 0 10px">4. Catat Setiap Makanan</h3>
<p style="margin-bottom:16px;line-height:1.8">Gunakan aplikasi seperti KaloriBerkah untuk mencatat semua makanan yang dikonsumsi. Penelitian menunjukkan bahwa orang yang mencatat makanannya berhasil menurunkan berat badan 2x lebih efektif.</p>`},
  {id:2,title:'10 Makanan Rendah Kalori tapi Kenyang',cat:'Tips Makan',emoji:'🥗',bg:'#FEF3C7',
   content:`<h2 style="font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800;margin-bottom:16px">10 Makanan Rendah Kalori tapi Kenyang</h2>
<p style="color:var(--text-muted);margin-bottom:20px">Diterbitkan 15 Januari 2024 • 4 menit baca</p>
<p style="margin-bottom:16px;line-height:1.8">Salah satu tantangan terbesar saat diet adalah rasa lapar. Berikut 10 makanan yang rendah kalori namun membuat kenyang lebih lama:</p>
<ol style="padding-left:20px">
<li style="margin-bottom:12px;line-height:1.8"><strong>Oatmeal (150 kcal/porsi)</strong> — Kaya serat beta-glucan yang membuat kenyang 2-3 jam</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Telur rebus (80 kcal/butir)</strong> — Protein tinggi yang supresi hormon lapar</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Sayur bayam (25 kcal/100g)</strong> — Volume tinggi, kalori sangat rendah</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Apel (52 kcal)</strong> — Serat pektin memperlambat pengosongan lambung</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Dada ayam rebus (110 kcal/100g)</strong> — Protein tertinggi, lemak minimal</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Tahu putih (75 kcal/100g)</strong> — Protein nabati yang mengenyangkan</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Nasi merah (111 kcal/100g)</strong> — GI rendah, bikin kenyang lebih lama vs nasi putih</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Ikan kukus (100 kcal/100g)</strong> — Protein tanpa lemak jahat</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Yogurt plain (60 kcal/100g)</strong> — Probiotik + protein</li>
<li style="margin-bottom:12px;line-height:1.8"><strong>Kacang rebus (100 kcal/porsi)</strong> — Serat + lemak sehat</li>
</ol>`},
  {id:3,title:'Manajemen Berat Badan untuk Pemula',cat:'Panduan',emoji:'💪',bg:'#DBEAFE',
   content:`<h2 style="font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800;margin-bottom:16px">Manajemen Berat Badan untuk Pemula</h2>
<p style="color:var(--text-muted);margin-bottom:20px">Diterbitkan 20 Januari 2024 • 6 menit baca</p>
<p style="margin-bottom:16px;line-height:1.8">Memulai perjalanan manajemen berat badan bisa terasa overwhelming. Artikel ini akan membantu Anda memulai dengan langkah yang tepat dan berkelanjutan.</p>
<h3 style="font-weight:700;margin:20px 0 10px">Prinsip Dasar: Caloric Balance</h3>
<p style="margin-bottom:16px;line-height:1.8">Hukum utama manajemen berat badan adalah keseimbangan kalori. Jika Anda mengonsumsi lebih banyak kalori dari yang dibakar, berat akan naik. Sebaliknya, defisit kalori menyebabkan penurunan berat badan.</p>
<h3 style="font-weight:700;margin:20px 0 10px">Langkah 1: Tentukan Tujuan yang Realistis</h3>
<p style="margin-bottom:16px;line-height:1.8">Targetkan penurunan 0.5-1 kg per minggu untuk hasil yang berkelanjutan. Penurunan lebih cepat sering menyebabkan kehilangan massa otot dan rebound effect.</p>
<h3 style="font-weight:700;margin:20px 0 10px">Langkah 2: Catat Semua Makanan</h3>
<p style="margin-bottom:16px;line-height:1.8">Gunakan log makanan selama minimal 2 minggu pertama. Banyak orang terkejut mengetahui berapa banyak kalori yang mereka konsumsi tanpa disadari.</p>
<h3 style="font-weight:700;margin:20px 0 10px">Langkah 3: Mulai Olahraga Sederhana</h3>
<p style="margin-bottom:16px;line-height:1.8">Mulai dengan 30 menit jalan cepat 3x seminggu. Secara bertahap tingkatkan intensitas dan durasi seiring tubuh beradaptasi.</p>`},
  {id:4,title:'Resep Sehat Murah di Bawah Rp 20.000',cat:'Resep',emoji:'🍳',bg:'#FCE7F3',
   content:`<h2 style="font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800;margin-bottom:16px">Resep Sehat Murah di Bawah Rp 20.000</h2>
<p style="color:var(--text-muted);margin-bottom:20px">Diterbitkan 25 Januari 2024 • 5 menit baca</p>
<p style="margin-bottom:16px;line-height:1.8">Makan sehat tidak harus mahal! Berikut 5 resep bergizi yang bisa Anda buat dengan budget di bawah Rp 20.000:</p>
<h3 style="font-weight:700;margin:20px 0 10px">1. Nasi Telur Tempe Tumis (±Rp 8.000)</h3>
<p style="margin-bottom:16px;line-height:1.8">Bahan: 1 porsi nasi, 2 butir telur, 100g tempe, bumbu dapur. Tumis tempe hingga kecokelatan, goreng telur, sajikan dengan nasi. Total: ±450 kcal, protein 25g.</p>
<h3 style="font-weight:700;margin:20px 0 10px">2. Sayur Sop Sederhana (±Rp 10.000)</h3>
<p style="margin-bottom:16px;line-height:1.8">Bahan: wortel, kentang, kol, buncis, sosis/bakso, bumbu. Rebus semua bahan dengan bumbu. Total: ±200 kcal, kaya vitamin.</p>
<h3 style="font-weight:700;margin:20px 0 10px">3. Pepes Tahu + Nasi (±Rp 12.000)</h3>
<p style="margin-bottom:16px;line-height:1.8">Bungkus tahu cincang dengan daun pisang, bumbu halus, dan kukus 20 menit. Sangat lezat dan bergizi!</p>
<h3 style="font-weight:700;margin:20px 0 10px">4. Omelet Sayur (±Rp 7.000)</h3>
<p style="margin-bottom:16px;line-height:1.8">2 butir telur + sisa sayur apapun di kulkas. Kocok telur, masukkan sayuran, masak di teflon. Cepat, murah, bergizi.</p>`},
  {id:5,title:'Tips Diet Tanpa Lapar',cat:'Tips Diet',emoji:'🎯',bg:'#F0FDF4',
   content:`<h2 style="font-family:'Sora',sans-serif;font-size:1.8rem;font-weight:800;margin-bottom:16px">Tips Diet Tanpa Lapar</h2>
<p style="color:var(--text-muted);margin-bottom:20px">Diterbitkan 1 Februari 2024 • 5 menit baca</p>
<p style="margin-bottom:16px;line-height:1.8">Diet tidak harus identik dengan lapar dan tersiksa. Dengan strategi yang tepat, Anda bisa defisit kalori sambil tetap merasa kenyang dan berenergi.</p>
<h3 style="font-weight:700;margin:20px 0 10px">1. Prioritaskan Protein</h3>
<p style="margin-bottom:16px;line-height:1.8">Protein adalah makronutrien paling mengenyangkan. Pastikan setiap makan mengandung sumber protein: telur, ayam, ikan, tahu, atau tempe.</p>
<h3 style="font-weight:700;margin:20px 0 10px">2. Perbanyak Sayur dan Buah</h3>
<p style="margin-bottom:16px;line-height:1.8">Sayuran volume tinggi (bayam, selada, timun) sangat rendah kalori tapi mengisi perut. Tambahkan ke setiap makan.</p>
<h3 style="font-weight:700;margin:20px 0 10px">3. Minum Air Sebelum Makan</h3>
<p style="margin-bottom:16px;line-height:1.8">Minum 1-2 gelas air 15 menit sebelum makan terbukti mengurangi jumlah makanan yang dikonsumsi hingga 13%.</p>
<h3 style="font-weight:700;margin:20px 0 10px">4. Makan Perlahan dan Mindful</h3>
<p style="margin-bottom:16px;line-height:1.8">Otak butuh 20 menit untuk menerima sinyal kenyang dari perut. Kunyah makanan 20-30 kali dan nikmati setiap gigitan.</p>
<h3 style="font-weight:700;margin:20px 0 10px">5. Pilih Karbohidrat Kompleks</h3>
<p style="margin-bottom:16px;line-height:1.8">Nasi merah, oatmeal, ubi, dan roti gandum punya indeks glikemik rendah sehingga gula darah stabil dan Anda kenyang lebih lama.</p>`},
];

function renderBlogGrid() {
  const grid = document.getElementById('blogGrid');
  grid.innerHTML = blogPosts.map(p=>`
    <div class="blog-card" onclick="showBlogDetail(${p.id})">
      <div class="blog-img" style="background:${p.bg}">${p.emoji}</div>
      <div class="blog-body">
        <div class="blog-cat">${p.cat}</div>
        <div class="blog-title">${p.title}</div>
        <div class="blog-excerpt">${p.content.replace(/<[^>]+>/g,'').substring(100,200)}...</div>
        <div class="blog-meta"><span>📅 Jan 2024</span><span>📖 5 mnt baca</span></div>
      </div>
    </div>`).join('');
}

function showBlogDetail(id) {
  const post = blogPosts.find(p=>p.id===id);
  if(!post) return;
  document.getElementById('blogList').classList.add('hidden');
  document.getElementById('blogDetail').classList.remove('hidden');
  document.getElementById('blogDetailContent').innerHTML = `
    <div class="card" style="max-width:800px;margin:0 auto">
      <div style="background:${post.bg};border-radius:12px;height:200px;display:flex;align-items:center;justify-content:center;font-size:72px;margin-bottom:24px">${post.emoji}</div>
      ${post.content}
      <div class="divider"></div>
      <div class="flex gap-2">
        <button class="btn btn-outline btn-sm" onclick="shareToWA('${encodeURIComponent(post.title)}')">📱 Share WhatsApp</button>
      </div>
    </div>`;
}

function backToBlogList() {
  document.getElementById('blogList').classList.remove('hidden');
  document.getElementById('blogDetail').classList.add('hidden');
}

function shareToWA(title) {
  window.open(`https://wa.me/?text=${decodeURIComponent(title)}%20-%20KaloriBerkah%20https://kaloriberkah.id`,'_blank');
}

// ========== FORUM ==========
const defaultTopics = [
  {id:1,author:'BudiSehat',title:'Tips Diet Ramadan tanpa Lemas',cat:'diet',content:'Hai semua! Mau share tips diet selama Ramadan yang sudah saya coba. Kuncinya adalah memilih makanan yang tepat saat sahur...',time:'2 jam lalu',replies:12,likes:45},
  {id:2,author:'SariWijaya',title:'Resep Salad Ayam Keto yang Enak Banget!',cat:'resep',content:'Akhirnya nemuin resep salad ayam keto yang nggak hambar! Rahasianya di saus dressing-nya yang pakai olive oil dan lemon...',time:'5 jam lalu',replies:8,likes:32},
  {id:3,author:'FitnessFam',title:'30 Hari Catat Kalori - Hasilku',cat:'motivasi',content:'Alhamdulillah selesai challenge 30 hari catat kalori di KaloriBerkah! Total turun 4 kg dan badan rasanya lebih enteng...',time:'1 hari lalu',replies:23,likes:87},
  {id:4,author:'HealthyMom',title:'Cara masak MPASI bergizi rendah sodium',cat:'resep',content:'Untuk para mama yang lagi MPASI, sini share resep yang bergizi dan rendah sodium untuk bayi 6-12 bulan...',time:'2 hari lalu',replies:15,likes:56},
  {id:5,author:'GymBro88',title:'Suplemen apa yang worth it untuk pemula gym?',cat:'diet',content:'Mau mulai gym serius nih, tapi bingung soal suplemen. Ada yang mau share pengalaman? Protein shake perlu nggak sih kalau baru mulai?',time:'3 hari lalu',replies:31,likes:44},
];

function getForumTopics() {
  return [...defaultTopics, ...appState.forumTopics];
}

function renderForum(filter) {
  const topics = getForumTopics().filter(t=>filter==='all'||t.cat===filter);
  document.getElementById('forumList').innerHTML = topics.map(t=>`
    <div class="forum-item">
      <div class="forum-avatar">${t.author.substring(0,2).toUpperCase()}</div>
      <div class="forum-content">
        <div class="forum-title">${t.title}</div>
        <div class="forum-preview">${t.content.substring(0,100)}...</div>
        <div class="forum-footer">
          <span>👤 ${t.author}</span>
          <span>💬 ${t.replies} balasan</span>
          <span>❤️ ${t.likes}</span>
          <span>🕐 ${t.time}</span>
        </div>
      </div>
    </div>`).join('');
}

function filterForum(el, cat) {
  document.querySelectorAll('.menu-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  renderForum(cat);
}

function openNewTopicModal() { openModal('newTopicModal'); }

function submitNewTopic() {
  const title = document.getElementById('topicTitle').value.trim();
  const content = document.getElementById('topicContent').value.trim();
  const author = document.getElementById('topicAuthor').value.trim() || 'Anonim';
  const cat = document.getElementById('topicCat').value;
  if(!title||!content){showToast('Lengkapi judul dan isi topik!','error');return;}
  appState.forumTopics.push({id:Date.now(),author,title,cat,content,time:'Baru saja',replies:0,likes:0});
  localStorage.setItem('forumTopics',JSON.stringify(appState.forumTopics));
  closeModal('newTopicModal');
  renderForum('all');
  showToast('✅ Topik berhasil diposting!','success');
}

// ========== DONASI ==========
const dummyDonatur = [
  {name:'Anonim',amount:'Rp 50.000',time:'2 menit lalu'},
  {name:'Ahmad R.',amount:'Rp 25.000',time:'15 menit lalu'},
  {name:'Sari W.',amount:'Rp 100.000',time:'1 jam lalu'},
  {name:'Anonim',amount:'Rp 10.000',time:'2 jam lalu'},
  {name:'Budi S.',amount:'Rp 50.000',time:'3 jam lalu'},
];

function renderDonasiPage() {
  const list = document.getElementById('donaturList');
  list.innerHTML = [...appState.donations.slice().reverse().slice(0,3), ...dummyDonatur].map(d=>`
    <div class="donatur-item">
      <div class="donatur-avatar">${(d.name||'A').substring(0,1)}</div>
      <div><div class="donatur-name">${d.name||'Anonim'}</div><div class="donatur-time">${d.time||'Baru saja'}</div></div>
      <div class="donatur-amount">${d.amount||d.nominal||''}</div>
    </div>`).join('');
  
  const myDiv = document.getElementById('myDonations');
  if(appState.donations.length){
    myDiv.innerHTML = appState.donations.map(d=>`
      <div class="donatur-item">
        <div class="donatur-avatar">💝</div>
        <div><div class="donatur-name">${d.nominal}</div><div class="donatur-time">${d.time}</div></div>
      </div>`).join('');
  }
}

function openDonasiModal() { openModal('donasiModal'); }

function selectNominal(el, amount) {
  document.querySelectorAll('.nominal-btn').forEach(b=>b.classList.remove('active'));
  el.classList.add('active');
  appState.currentDonation = amount;
  document.getElementById('customNominal').value='';
}

function clearNominalSelection() {
  document.querySelectorAll('.nominal-btn').forEach(b=>b.classList.remove('active'));
  appState.currentDonation = 0;
}

function submitDonasi() {
  const custom = parseFloat(document.getElementById('customNominal').value);
  const amount = custom || appState.currentDonation;
  if(!amount||amount<1000){showToast('Pilih atau masukkan nominal donasi!','error');return;}
  const name = document.getElementById('donaturName').value||'Anonim';
  const anon = document.getElementById('donasiAnon').checked;
  const nominal = `Rp ${amount.toLocaleString('id-ID')}`;
  const donation = {name:anon?'Anonim':name,amount:nominal,nominal,time:new Date().toLocaleTimeString('id-ID'),rawAmount:amount};
  appState.donations.push(donation);
  localStorage.setItem('donations',JSON.stringify(appState.donations));
  closeModal('donasiModal');
  document.getElementById('successNominal').textContent = `Donasi: ${nominal}`;
  openModal('donasiSuccessModal');
  addPoints(50);
  showToast('💝 Terima kasih atas donasi berkah Anda!','success');
  // Open donasi link
  const link = appState.donasiLink;
  if(link) setTimeout(()=>window.open(link,'_blank'),1500);
}

function generateDonasiCertificate() {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF({orientation:'landscape',unit:'mm',format:'a5'});
  doc.setFillColor(16,185,129);
  doc.rect(0,0,210,148,'F');
  doc.setFillColor(255,255,255);
  doc.roundedRect(10,10,190,128,5,5,'F');
  doc.setTextColor(16,185,129);
  doc.setFont('helvetica','bold');
  doc.setFontSize(22);
  doc.text('SERTIFIKAT DONASI BERKAH',105,35,'center');
  doc.setTextColor(100,100,100);
  doc.setFont('helvetica','normal');
  doc.setFontSize(12);
  doc.text('KaloriBerkah - Hitung Kalori, Sehatkan Tubuh, Berkahi Hidup',105,45,'center');
  const last = appState.donations[appState.donations.length-1];
  if(last){
    doc.setTextColor(30,30,30);
    doc.setFont('helvetica','bold');
    doc.setFontSize(14);
    doc.text(`Dengan bangga menyampaikan ucapan terima kasih kepada:`,105,65,'center');
    doc.setFontSize(18);
    doc.setTextColor(16,185,129);
    doc.text(last.name,105,78,'center');
    doc.setFontSize(13);
    doc.setTextColor(30,30,30);
    doc.text(`atas donasi sebesar ${last.nominal}`,105,90,'center');
  }
  doc.setFontSize(10);
  doc.setTextColor(100,100,100);
  doc.text(`Semoga menjadi berkah yang berlipat ganda. Aamiin.`,105,105,'center');
  doc.text(`${new Date().toLocaleDateString('id-ID',{day:'numeric',month:'long',year:'numeric'})}`,105,115,'center');
  doc.save('sertifikat-donasi-kaloriberkah.pdf');
  showToast('📄 Sertifikat berhasil didownload!','success');
}

function shareWhatsApp() {
  const last = appState.donations[appState.donations.length-1];
  const msg = `Alhamdulillah, saya baru saja berdonasi ${last?.nominal||''} di KaloriBerkah 💝\n\n"Sehatkan tubuh, berkahi hidup"\n\nYuk ikut berdonasi: ${appState.donasiLink}`;
  window.open(`https://wa.me/?text=${encodeURIComponent(msg)}`, '_blank');
  closeModal('donasiSuccessModal');
}

// ========== SETTINGS ==========
function loadSettingsData() {
  const p = appState.userProfile;
  if(p.name) document.getElementById('sName').value=p.name||'';
  if(p.age) document.getElementById('sAge').value=p.age||'';
  if(p.gender) document.getElementById('sGender').value=p.gender||'male';
  if(p.weight) document.getElementById('sWeight').value=p.weight||'';
  if(p.height) document.getElementById('sHeight').value=p.height||'';
  document.getElementById('sTargetKcal').value=appState.targetKcal;
  document.getElementById('sTargetWater').value=appState.targetWater;
}

function saveSettings() {
  const data = {
    name:document.getElementById('sName').value,
    age:document.getElementById('sAge').value,
    gender:document.getElementById('sGender').value,
    weight:document.getElementById('sWeight').value,
    height:document.getElementById('sHeight').value,
    diet:document.getElementById('sDiet').value,
  };
  Object.assign(appState.userProfile, data);
  localStorage.setItem('userProfile',JSON.stringify(appState.userProfile));
  showToast('✅ Profil berhasil disimpan!','success');
}

function saveTargetSettings() {
  const kcal = parseInt(document.getElementById('sTargetKcal').value);
  const water = parseInt(document.getElementById('sTargetWater').value);
  if(kcal>0) {appState.targetKcal=kcal;localStorage.setItem('targetKcal',kcal);}
  if(water>0) {appState.targetWater=water;localStorage.setItem('targetWater',water);}
  showToast('✅ Target kalori diperbarui!','success');
}

function showSettingsTab(id, el) {
  document.querySelectorAll('[id^="settings-"]').forEach(s=>s.classList.add('hidden'));
  document.getElementById('settings-'+id).classList.remove('hidden');
  document.querySelectorAll('.settings-nav a').forEach(a=>a.classList.remove('active'));
  el.classList.add('active');
}

function exportDataUser() {
  const data = {profile:appState.userProfile,log:appState.todayLog,donations:appState.donations,points:appState.points};
  const blob = new Blob([JSON.stringify(data,null,2)],{type:'application/json'});
  const a = document.createElement('a');
  a.href=URL.createObjectURL(blob);
  a.download='kaloriberkah-data.json';
  a.click();
  showToast('📥 Data berhasil didownload!','success');
}

function clearAllData() {
  localStorage.clear();
  appState = {targetKcal:1800,targetWater:8,todayLog:[],waterCount:0,weeklyData:[],userProfile:{},points:0,badges:['pemula'],donations:[],donasiLink:'',currentDonation:0,selectedFood:null,currentMenuPaket:null,forumTopics:[],adminLoggedIn:false};
  showToast('🗑️ Semua data dihapus','warning');
}

// ========== GAMIFIKASI ==========
function addPoints(pts) {
  appState.points += pts;
  localStorage.setItem('points',appState.points);
  const el = document.getElementById('userPoints');
  if(el) el.textContent = appState.points + ' Poin';
  const lvl = document.getElementById('userLevel');
  if(lvl) lvl.textContent = getLevel(appState.points);
}

function getLevel(pts) {
  if(pts>=1000) return 'Legenda';
  if(pts>=500) return 'Master';
  if(pts>=200) return 'Ahli';
  if(pts>=50) return 'Aktif';
  return 'Pemula';
}

// ========== ADMIN ==========
function adminLogin() {
  const u = document.getElementById('adminUser').value;
  const p = document.getElementById('adminPass').value;
  if(u==='admin'&&p==='admin123'){
    appState.adminLoggedIn=true;
    showPage('admin');
    showToast('✅ Login admin berhasil!','success');
  } else {
    showToast('Username atau password salah!','error');
  }
}

function adminLogout() {
  appState.adminLoggedIn=false;
  showPage('home');
  showToast('Logout berhasil','');
}

function initAdmin() {
  if(!appState.adminLoggedIn){showPage('adminLogin');return;}
  document.getElementById('adminDate').textContent=new Date().toLocaleDateString('id-ID',{weekday:'long',day:'numeric',month:'long',year:'numeric'});
  document.getElementById('adminFoodCount').textContent=foodDatabase.length;
  document.getElementById('adminTotalCalc').textContent=(appState.todayLog.reduce((s,f)=>s+f.kcal,0)||0).toLocaleString();
  renderAdminFoodTable();
  renderAdminChart();
  renderAdminMenus();
  renderAdminBadges();
  document.getElementById('donasiLink').value=appState.donasiLink;
  renderAdminDonasi();
  const inputs = document.getElementById('statCalcInput');
  if(inputs) inputs.value = document.getElementById('statCalc')?.textContent||'';
}

function showAdminSection(id) {
  document.querySelectorAll('[id^="admin-"]').forEach(s=>{if(s.id!=='admin-dashboard'||id==='dashboard')s.classList.add('hidden')});
  document.getElementById('admin-'+id).classList.remove('hidden');
  document.querySelectorAll('.admin-nav a').forEach(a=>a.classList.remove('active'));
  event.target.closest('a').classList.add('active');
}

function renderAdminFoodTable() {
  const q=(document.getElementById('adminFoodSearch')?.value||'').toLowerCase();
  const filtered=foodDatabase.filter(f=>!q||f.name.toLowerCase().includes(q));
  document.getElementById('adminFoodTable').innerHTML=filtered.map((f,i)=>`
    <tr>
      <td>${i+1}</td>
      <td>${f.emoji} ${f.name}</td>
      <td>${f.kcal}</td>
      <td>${f.protein}g</td>
      <td>${f.karbo}g</td>
      <td>${f.lemak}g</td>
      <td><span class="tag tag-green">${f.cat}</span></td>
      <td>
        <button class="btn btn-outline btn-sm" onclick="editFood(${f.id})" style="margin-right:4px">✏️</button>
        <button class="btn btn-danger btn-sm" onclick="deleteFood(${f.id})">🗑️</button>
      </td>
    </tr>`).join('');
}

function openAddFoodModal(editId=-1) {
  document.getElementById('af_editIndex').value=editId;
  document.getElementById('foodModalTitle').textContent = editId>0 ? '✏️ Edit Makanan' : '➕ Tambah Makanan';
  if(editId>0){
    const f=foodDatabase.find(x=>x.id===editId);
    if(f){
      document.getElementById('af_name').value=f.name;
      document.getElementById('af_kcal').value=f.kcal;
      document.getElementById('af_protein').value=f.protein;
      document.getElementById('af_karbo').value=f.karbo;
      document.getElementById('af_lemak').value=f.lemak;
      document.getElementById('af_cat').value=f.cat;
      document.getElementById('af_emoji').value=f.emoji||'🍽️';
    }
  } else {
    ['af_name','af_kcal','af_protein','af_karbo','af_lemak','af_emoji'].forEach(id=>document.getElementById(id).value='');
  }
  openModal('addFoodModal');
}

function editFood(id) { openAddFoodModal(id); }

function deleteFood(id) {
  if(!confirm('Hapus item ini?')) return;
  foodDatabase = foodDatabase.filter(f=>f.id!==id);
  renderAdminFoodTable();
  document.getElementById('adminFoodCount').textContent=foodDatabase.length;
  showToast('🗑️ Item dihapus','warning');
}

function saveFoodItem() {
  const name=document.getElementById('af_name').value.trim();
  const kcal=parseFloat(document.getElementById('af_kcal').value);
  if(!name||!kcal){showToast('Nama dan kalori wajib diisi!','error');return;}
  const editId=parseInt(document.getElementById('af_editIndex').value);
  const item={
    id:editId>0?editId:Date.now(),
    name, kcal,
    protein:parseFloat(document.getElementById('af_protein').value)||0,
    karbo:parseFloat(document.getElementById('af_karbo').value)||0,
    lemak:parseFloat(document.getElementById('af_lemak').value)||0,
    cat:document.getElementById('af_cat').value,
    emoji:document.getElementById('af_emoji').value||'🍽️',
    unit:'100g', tags:[]
  };
  if(editId>0){const idx=foodDatabase.findIndex(f=>f.id===editId);if(idx>-1)foodDatabase[idx]=item;}
  else foodDatabase.push(item);
  closeModal('addFoodModal');
  renderAdminFoodTable();
  document.getElementById('adminFoodCount').textContent=foodDatabase.length;
  showToast('✅ Data makanan disimpan!','success');
}

let adminChartInstance;
function renderAdminChart() {
  const ctx=document.getElementById('adminChart');
  if(!ctx) return;
  if(adminChartInstance) adminChartInstance.destroy();
  const days=['Sen','Sel','Rab','Kam','Jum','Sab','Min'];
  const data=[1820,1650,2100,1780,1920,1450,1800];
  adminChartInstance=new Chart(ctx,{type:'bar',data:{labels:days,datasets:[{label:'Rata-rata Kalori (kcal)',data,backgroundColor:'rgba(16,185,129,.7)',borderColor:'#10B981',borderWidth:2,borderRadius:6}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{beginAtZero:false,min:1000,grid:{color:'rgba(0,0,0,.05)'}},x:{grid:{display:false}}}}});
}

function renderAdminMenus() {
  const c=document.getElementById('adminMenuContent');
  if(!c) return;
  let h='<div style="display:flex;flex-direction:column;gap:16px">';
  Object.entries(menuData).forEach(([key,pkg])=>{
    h+=`<div class="card"><div class="flex items-center justify-between mb-2">
      <div><strong>${pkg.title}</strong> — ${pkg.items.length} item, Target: ${pkg.target}</div>
    </div><div style="display:flex;flex-wrap:wrap;gap:8px">${pkg.items.map(i=>`<span class="tag tag-green">${i.emoji} ${i.name} (${i.kcal} kcal)</span>`).join('')}</div></div>`;
  });
  h+='</div>';
  c.innerHTML=h;
}

function renderAdminBadges() {
  const badges=[
    {icon:'🌱',name:'Pemula',desc:'Pertama kali catat kalori'},
    {icon:'🔥',name:'Konsisten 7 Hari',desc:'Catat 7 hari berturut-turut'},
    {icon:'💝',name:'Donatur Berkah',desc:'Pertama kali berdonasi'},
    {icon:'🍳',name:'Resep Baru',desc:'Coba 5 menu berbeda'},
    {icon:'⭐',name:'Sehat 30 Hari',desc:'30 hari tracking'},
  ];
  const grid=document.getElementById('adminBadgeGrid');
  if(!grid) return;
  grid.innerHTML=badges.map(b=>`
    <div class="badge-item earned">
      <div class="badge-icon">${b.icon}</div>
      <div class="badge-name">${b.name}</div>
      <div class="badge-desc">${b.desc}</div>
    </div>`).join('');
}

function renderAdminDonasi() {
  const tbody=document.getElementById('adminDonasiTable');
  if(!tbody) return;
  const all=[...appState.donations,...[
    {name:'Anonim',amount:'Rp 50.000',time:'Hari ini 08:30',status:'Selesai'},
    {name:'Ahmad R.',amount:'Rp 25.000',time:'Hari ini 07:15',status:'Selesai'},
  ]];
  tbody.innerHTML=all.map(d=>`<tr><td>${d.name||d.name}</td><td>${d.amount||d.nominal}</td><td>${d.time}</td><td><span class="tag tag-green">Selesai</span></td></tr>`).join('');
}

function saveDonasiLink() {
  const link=document.getElementById('donasiLink').value.trim();
  appState.donasiLink=link;
  localStorage.setItem('donasiLink',link);
  showToast('✅ Link donasi disimpan!','success');
}

function saveHeroStats() {
  const calc=document.getElementById('statCalcInput').value;
  const don=document.getElementById('statDonasiInput').value;
  if(calc) document.getElementById('statCalc').textContent=calc;
  if(don) document.getElementById('statDonasi').textContent=don;
  showToast('✅ Statistik hero diperbarui!','success');
}

// ========== MODALS ==========
function openModal(id) {
  document.getElementById(id).classList.add('show');
  document.body.style.overflow='hidden';
}
function closeModal(id) {
  document.getElementById(id).classList.remove('show');
  document.body.style.overflow='';
}
document.querySelectorAll('.modal-overlay').forEach(m=>{
  m.addEventListener('click',e=>{if(e.target===m) closeModal(m.id);});
});
document.addEventListener('keydown',e=>{if(e.key==='Escape') document.querySelectorAll('.modal-overlay.show').forEach(m=>closeModal(m.id));});

// ========== EXPORT LOG PDF ==========
function exportLogPDF() {
  if(!window.jspdf){showToast('PDF library loading...','warning');return;}
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();
  doc.setFont('helvetica','bold');
  doc.setFontSize(18);
  doc.setTextColor(16,185,129);
  doc.text('KaloriBerkah - Log Harian',20,20);
  doc.setFont('helvetica','normal');
  doc.setFontSize(11);
  doc.setTextColor(100);
  doc.text(`Tanggal: ${new Date().toLocaleDateString('id-ID')}`,20,30);
  doc.text(`Target Kalori: ${appState.targetKcal} kcal`,20,38);
  const total=appState.todayLog.reduce((s,f)=>s+f.kcal,0);
  doc.text(`Total Dikonsumsi: ${total} kcal`,20,46);
  doc.setFontSize(12);
  doc.setTextColor(30);
  let y=60;
  appState.todayLog.forEach((f,i)=>{
    doc.text(`${i+1}. ${f.name} - ${f.kcal} kcal (${f.category})`,20,y);
    y+=8; if(y>270){doc.addPage();y=20;}
  });
  doc.save('log-kaloriberkah.pdf');
  showToast('📥 Log berhasil diexport ke PDF!','success');
}

// ========== TOAST ==========
function showToast(msg, type='') {
  const container=document.getElementById('toastContainer');
  const toast=document.createElement('div');
  toast.className='toast '+(type==='error'?'error':type==='warning'?'warning':'');
  toast.innerHTML=`<span>${msg}</span>`;
  container.appendChild(toast);
  setTimeout(()=>toast.classList.add('show'),10);
  setTimeout(()=>{toast.classList.remove('show');setTimeout(()=>toast.remove(),400);},3500);
}

// ========== INIT ==========
document.addEventListener('DOMContentLoaded',()=>{
  renderBlogGrid();
  renderForum('all');
  initLogPage();
  // Load saved donasi link
  const savedLink = localStorage.getItem('donasiLink');
  if(savedLink) appState.donasiLink = savedLink;
});
</script>
</body>
</html>
