<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>BLUVEVA — Visite immersive</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400&family=Inter:wght@300;400&display=swap" rel="stylesheet">
<style>
:root{--ink:#eef3ff;--mut:#b4c2dc;--amb:#ffc98a;--bg:#05080f;color-scheme:dark}
*{box-sizing:border-box;margin:0}
body{background:var(--bg);color:var(--ink);font:300 1rem/1.6 Inter,system-ui,sans-serif}
#cv{position:fixed;inset:0;width:100%;height:100%;display:block}
body::after{content:"";position:fixed;inset:0;pointer-events:none;background:radial-gradient(ellipse at center,transparent 45%,rgba(2,4,10,.7))}
header{position:fixed;top:0;left:0;z-index:5;padding:calc(env(safe-area-inset-top,0px) + 20px) 28px;font:400 1rem "Cormorant Garamond",serif;letter-spacing:.4em;pointer-events:none}
.c{position:fixed;inset:0;z-index:4;display:flex;flex-direction:column;justify-content:center;align-items:flex-start;padding:0 8vw;opacity:0;pointer-events:none;text-shadow:0 2px 28px rgba(0,0,0,.7)}
.c.r{align-items:flex-end;text-align:right}
.c.m{align-items:center;text-align:center}
.c small{font-size:.95rem;color:var(--amb);display:flex;align-items:center;gap:14px}
.c small::before{content:"";width:44px;height:1px;background:var(--amb)}
.c.m small::before{display:none}
.c h2{font:300 clamp(2.2rem,6.5vw,5rem)/1.05 "Cormorant Garamond",serif;margin:.35em 0 .45em;max-width:14em}
.c.h h2{font-size:clamp(2.6rem,12vw,8.5rem);letter-spacing:.22em;margin-right:-.22em}
.c p{max-width:27em;color:var(--mut);font-size:1.05rem}
.btn{margin-top:2rem;font:400 .95rem Inter,sans-serif;color:var(--ink);background:rgba(255,201,138,.12);border:1px solid var(--amb);padding:.9rem 1.8rem;cursor:pointer;backdrop-filter:blur(6px)}
.btn:hover,.btn:focus-visible{background:var(--amb);color:#1a1208;outline:none}
.c.on .btn{pointer-events:auto}
#cue{position:fixed;z-index:5;left:0;right:0;bottom:56px;text-align:center;color:var(--mut);font-size:.9rem;pointer-events:none}
#bar{position:fixed;z-index:5;left:0;right:0;bottom:0;height:2px;background:rgba(255,255,255,.1)}
#bar i{display:block;height:100%;background:var(--amb);transform-origin:left;transform:scaleX(0)}
footer{position:fixed;z-index:5;left:28px;bottom:14px;font-size:.75rem;color:#7d8aa5;pointer-events:none}
#menu{position:fixed;z-index:6;left:0;right:0;bottom:44px;display:none;flex-wrap:wrap;gap:10px;justify-content:center;padding:0 16px}#menu.on{display:flex}
#menu button,#back{font:400 .9rem Inter,sans-serif;color:var(--ink);background:rgba(8,14,28,.66);border:1px solid var(--amb);padding:.8rem 1.3rem;cursor:pointer;backdrop-filter:blur(8px)}
#menu button:hover,#back:hover,#menu button:focus-visible,#back:focus-visible{background:var(--amb);color:#1a1208;outline:none}
#say{position:fixed;z-index:6;left:50%;top:16%;transform:translateX(-50%);width:max-content;max-width:min(30em,88vw);padding:1rem 1.4rem;background:rgba(8,14,28,.72);border-left:2px solid var(--amb);backdrop-filter:blur(8px);opacity:0;transition:opacity .6s;pointer-events:none}#say.on{opacity:1}
#say b{font:400 1.5rem "Cormorant Garamond",serif}
#back{position:fixed;z-index:6;right:20px;top:calc(env(safe-area-inset-top,0px) + 16px);display:none}#back.on{display:block}
#cv{filter:contrast(1.1) saturate(1.12)}
body::before{content:"";position:fixed;inset:0;z-index:3;pointer-events:none;opacity:.14;mix-blend-mode:overlay;background-image:url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='200' height='200'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='2'/></filter><rect width='200' height='200' filter='url(%23n)'/></svg>");animation:gr .6s steps(3) infinite}
@keyframes gr{0%{background-position:0 0}33%{background-position:-60px 40px}66%{background-position:40px -70px}100%{background-position:0 0}}
@media (prefers-reduced-motion:reduce){body::before{animation:none}}
@media (min-aspect-ratio:1/1){body::after{box-shadow:inset 0 6vh 0 0 #000,inset 0 -6vh 0 0 #000}}
#shop{position:fixed;z-index:6;right:20px;top:90px;width:min(22rem,calc(100vw - 40px));max-height:calc(100vh - 160px);overflow:auto;padding:1.2rem;background:rgba(8,14,28,.8);border:1px solid rgba(255,201,138,.35);backdrop-filter:blur(10px);display:none}#shop.on{display:block}
#shop h3{font:400 1.6rem "Cormorant Garamond",serif;margin-bottom:.4rem}
#shop p{color:var(--mut);font-size:.9rem}
#shop .o{display:block;width:100%;text-align:left;margin:.45rem 0;padding:.7rem .9rem;color:var(--ink);background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.18);cursor:pointer;font:400 .95rem Inter,sans-serif}
#shop .o small{display:block;color:var(--mut);font-size:.8rem;font-weight:300}
#shop .o.sel{border-color:var(--amb);background:rgba(255,201,138,.16)}
#shop .go{width:100%;margin-top:.8rem;padding:.8rem;font:400 .95rem Inter,sans-serif;color:#1a1208;background:var(--amb);border:0;cursor:pointer}#shop .go:disabled{opacity:.4;cursor:default}
@media (max-width:700px){#shop{top:auto;bottom:0;right:0;left:0;width:auto;max-height:42vh}}
#fade{position:fixed;inset:0;z-index:8;background:#000;opacity:0;pointer-events:none;transition:opacity .6s}
#err{position:fixed;z-index:9;inset:0;display:grid;place-items:center;padding:2rem;text-align:center;background:var(--bg)}
#err[hidden]{display:none}
</style>
</head>
<body>
<canvas id="cv"></canvas>
<header>BLUVEVA</header>
<div id="ch"></div>
<div id="say"></div><div id="shop"></div><div id="menu"></div><button id="back">Retour au hall</button><div id="fade"></div>
<div id="cue">Faites défiler pour avancer</div>
<div id="bar"><i></i></div>
<footer>Démonstration de concept, scène 3D calculée en direct dans votre navigateur</footer>
<div id="err" hidden>Votre navigateur ne peut pas afficher la 3D (WebGL). Essayez Chrome, Edge ou Firefox récents.</div>
<div id="s" style="height:500vh"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
const $=id=>document.getElementById(id);
let R;
try{R=new THREE.WebGLRenderer({canvas:$('cv'),antialias:true})}catch(e){$('err').hidden=false;throw e}
R.setPixelRatio(Math.min(devicePixelRatio,1.75));
R.toneMapping=THREE.ACESFilmicToneMapping;R.toneMappingExposure=1.15;
const S=new THREE.Scene(),K=new THREE.PerspectiveCamera(55,1,.1,900);

/* textures dessinées en code */
const tex=(w,h,f)=>{const c=document.createElement('canvas');c.width=w;c.height=h;f(c.getContext('2d'),w,h);return new THREE.CanvasTexture(c)};
S.background=tex(4,512,(g,w,h)=>{const l=g.createLinearGradient(0,0,0,h);
 l.addColorStop(0,'#03060d');l.addColorStop(.5,'#14264a');l.addColorStop(.88,'#6d5470');l.addColorStop(1,'#e8955e');g.fillStyle=l;g.fillRect(0,0,w,h)});
S.fog=new THREE.FogExp2(0x182544,.004);
const WT=tex(256,64,(g,w,h)=>{g.fillStyle='#0d1424';g.fillRect(0,0,w,h);
 for(let i=0;i<16;i++){g.fillStyle=Math.random()<.65?`hsl(${30+Math.random()*15},90%,${55+Math.random()*20}%)`:'#2a3b5c';g.fillRect(i*16+1,4,14,h-8)}});
WT.wrapS=WT.wrapT=THREE.RepeatWrapping;WT.repeat.set(2,1);

/* matériaux */
const mat=(c,r,m)=>new THREE.MeshStandardMaterial({color:c,roughness:r,metalness:m}),bas=c=>new THREE.MeshBasicMaterial({color:c});
const M={con:mat(0xd8d4cc,.55,.05),dark:mat(0x0a0f1a,.3,.6),floor:mat(0x0c111b,.12,.8),ground:mat(0x080c14,.5,.3),pool:mat(0x04101f,.03,.9),
 glass:new THREE.MeshPhysicalMaterial({color:0x8cc0e8,roughness:.05,metalness:.2,transparent:true,opacity:.22,depthWrite:false}),
 warm:bas(0xffd6a0),blue:bas(0x5cbcff),rpool:bas(0x2fa8f0),
 win:new THREE.MeshBasicMaterial({map:WT,color:0xbbbbbb}),city:new THREE.MeshBasicMaterial({map:WT,color:0x7f90b4}),
 haze:new THREE.MeshBasicMaterial({color:0x9fc8ff,transparent:true,opacity:.07,side:THREE.DoubleSide,blending:THREE.AdditiveBlending,depthWrite:false})};
const add=(g,m,x,y,z)=>{const o=new THREE.Mesh(g,m);o.position.set(x,y,z);S.add(o);return o};
const bx=(w,h,d,m,x,y,z)=>add(new THREE.BoxGeometry(w,h,d),m,x,y,z);

/* sol, bassin, lignes de lumière vers l’entrée */
bx(900,.1,900,M.ground,0,-.05,0);
bx(26,.06,44,M.pool,0,.03,40);
[-1,1].forEach(s=>{bx(.2,.08,44,M.warm,s*13.1,.06,40);bx(.12,.03,70,M.warm,s*4,.1,45)});

/* hall en double hauteur */
bx(26,.2,16.4,M.floor,0,.1,0);
bx(26,.4,16.4,M.con,0,6.8,0);
for(let i=0;i<5;i++)bx(.25,.05,15,M.warm,-9+i*4.5,6.55,0);
[-1,1].forEach(s=>{
 [[2.4,-6.8],[4.8,0],[2.4,6.8]].forEach(([l,z])=>bx(.4,7,l,M.con,s*13,3.5,z));[-4,4].forEach(z=>bx(.4,2.4,3.2,M.con,s*13,5.8,z));
 bx(7,7,.5,M.con,s*9.5,3.5,-8);
 bx(10.5,7,.2,M.glass,s*7.75,3.5,8);
 [5,0,-5].forEach(z=>add(new THREE.CylinderGeometry(.35,.35,6.8,20),M.con,s*7,3.4,z));
});
bx(12,1.6,.5,M.con,0,6,-8);
bx(5,1.8,.3,M.dark,0,6.1,8.1);
bx(5,1.1,1.6,M.dark,-5,.65,-4);bx(5,.06,1.65,M.blue,-5,1.22,-4);
[6,2,-2,-6].forEach(z=>{add(new THREE.SphereGeometry(.3,16,12),M.warm,0,5.2,z);add(new THREE.CylinderGeometry(.015,.015,1.6),M.dark,0,6.1,z)});

/* personnages, portes et salles de services */
let mode='walk',tw=null,cur=-1,st=0,hT=0,dt=0,T=0;const clk=new THREE.Clock();
const skin=bas(0xe0b48f),hairM=mat(0x2a1a14,.8,0);
const shM=new THREE.MeshBasicMaterial({map:tex(64,64,g=>{const r=g.createRadialGradient(32,32,0,32,32,32);r.addColorStop(0,'rgba(0,0,0,.7)');r.addColorStop(1,'rgba(0,0,0,0)');g.fillStyle=r;g.fillRect(0,0,64,64)}),transparent:true,depthWrite:false});
function P(x,z,col,ry,sit,hat){const g=new THREE.Group(),m=mat(col,.7,0);
 const pt=(geo,mt,px,py,pz,par)=>{const o=new THREE.Mesh(geo,mt);o.position.set(px,py,pz);(par||g).add(o);return o};
 pt(new THREE.CylinderGeometry(.2,.24,.75,12),m,0,1.15,0);pt(new THREE.SphereGeometry(.15,12,10),skin,0,1.69,0);
 if(hat)pt(new THREE.SphereGeometry(.18,12,8,0,6.3,0,1.6),bas(hat),0,1.72,0);else pt(new THREE.SphereGeometry(.16,12,8),hairM,0,1.73,-.03);
 const lg=new THREE.Group();lg.position.y=.8;g.add(lg);[-.1,.1].forEach(s=>pt(new THREE.CylinderGeometry(.1,.09,.8,8),M.dark,s,-.4,0,lg));
 g.arms=[-.3,.3].map(s=>{const a=new THREE.Group();a.position.set(s,1.45,0);g.add(a);pt(new THREE.CylinderGeometry(.06,.06,.6,8),m,0,-.3,0,a);return a});
 g.legs=lg;g.position.set(x,sit?-.2:.2,z);g.rotation.y=ry||0;if(sit)lg.rotation.x=-1.5;const sh=new THREE.Mesh(new THREE.PlaneGeometry(.9,.9),shM);sh.rotation.x=-Math.PI/2;sh.position.y=sit?.42:.02;g.add(sh);g.sh=sh;S.add(g);return g}
const LB=[];
function lab(txt,w,h,x,y,zz,ry){const c=document.createElement('canvas');c.width=512;c.height=96;const g=c.getContext('2d'),tt=new THREE.CanvasTexture(c);
 const d=()=>{g.clearRect(0,0,512,96);g.fillStyle='#fff';g.font='400 36px "Cormorant Garamond",serif';g.textAlign='center';g.textBaseline='middle';g.fillText(txt,256,50);tt.needsUpdate=true};
 d();LB.push(d);const m=add(new THREE.PlaneGeometry(w,h),new THREE.MeshBasicMaterial({map:tt,transparent:true}),x,y,zz);m.rotation.y=ry;return m}
if(document.fonts)document.fonts.ready.then(()=>LB.forEach(f=>f()));
const ad=(g,geo,mt,x,y,zz,rx)=>{const o=new THREE.Mesh(geo,mt);o.position.set(x,y,zz);o.rotation.x=rx||0;g.add(o)};
const RL=new THREE.PointLight(0xfff0dd,0,34);S.add(RL);
/* accueil : Léa, assise derrière son bureau */
const Sg=P(-5,-5.4,0x1c2a4a,0,1);bx(.6,.1,.6,M.dark,-5,.5,-5.5);bx(.6,.7,.1,M.dark,-5,.9,-5.9);bx(.7,.45,.05,M.blue,-5,1.55,-4.5);
const SV=[
 {n:'Construction & rénovation',t:'Maçonnerie, gros œuvre, finitions : nos équipes montent et rénovent vos bâtiments, brique après brique.',sx:-1,z:4,c:0xffb347},
 {n:'Digital & informatique',t:'Sites, applications, réseaux : nos développeurs conçoivent, codent et maintiennent vos outils numériques.',sx:-1,z:-4,c:0x4fc3ff},
 {n:'Conseil & gestion',t:'Stratégie, comptabilité, suivi de projets : nous analysons vos chiffres pour décider avec vous.',sx:1,z:-4,c:0x7be0a4},
 {n:'Entretien & nettoyage',t:'Bureaux, vitres, parties communes : des équipes régulières pour des lieux toujours impeccables.',sx:1,z:4,c:0x9fe8ff}];
[-1,1].forEach(s=>bx(20,6,.4,M.con,s*23,3,0));
SV.forEach((v,k)=>{const s=v.sx,z=v.z,A=bas(v.c),f=s*Math.PI/2;let u=()=>{};
 bx(20,.2,8,M.floor,s*23,.1,z);bx(20,.3,8,M.con,s*23,6.2,z);bx(.4,6,8,M.con,s*33,3,z);bx(20,6,.4,M.con,s*23,3,z*2);
 for(let i=0;i<4;i++)bx(.2,.05,7,A,s*(16+i*5),6,z);
 bx(.5,.15,3.6,A,s*12.9,4.65,z);[-1,1].forEach(q=>bx(.5,4.6,.12,A,s*12.9,2.3,z+q*1.7));
 v.dp=[bx(.12,4.6,1.6,M.dark,s*12.7,2.3,z),bx(.12,4.6,1.6,M.dark,s*12.7,2.3,z)];v.o=0;v.g=0;
 lab(v.n,3.2,.6,s*12.7,5.85,z,-s*Math.PI/2);
 if(k==0){const br=[];for(let r=0;r<4;r++)for(let c=0;c<5;c++)br.push(Object.assign(bx(.5,.25,1.1,mat(0xb4553a,.8,0),s*31,.33+r*.26,z-2.5+c*1.15+(r%2)*.5),{y0:.33+r*.26}));
  [-3,3].forEach(q=>add(new THREE.CylinderGeometry(.05,.05,4.4),A,s*26,2.2,z+q));bx(.8,.08,6.2,A,s*26,2.4,z);
  const w1=P(s*29.4,z,0xe8a33d,f,0,0xffd23d),w2=P(s*24,z,0x3d6fe8,0,0,0xffffff);
  u=t=>{br.forEach((b,i)=>{const q=Math.max(.001,Math.min(1,t*1.5%26-i));b.scale.y=q;b.position.y=b.y0-.125*(1-q)});
   w1.arms[1].rotation.x=-1.2+Math.sin(t*6)*.5;w1.arms[0].rotation.x=-1;
   w2.position.z=z+Math.sin(t*.8)*2.2;w2.arms[0].rotation.x=w2.arms[1].rotation.x=-1.1;w2.rotation.y=Math.cos(t*.8)>0?0:Math.PI}}
 if(k==1){const dv=[-2.5,0,2.5].map((q,i)=>{bx(1.1,.08,2,M.dark,s*30,1,z+q);bx(.08,.6,1,A,s*30.4,1.4,z+q);bx(.5,.45,.5,M.dark,s*29,.4,z+q);return P(s*29,z+q,[0x3a4a6a,0x6a3a5a,0x2a5a5a][i],f,1)});
  const hk=add(new THREE.TorusKnotGeometry(.6,.17,80,10),new THREE.MeshBasicMaterial({color:v.c,wireframe:true}),s*21,2.4,z);bx(.8,.1,.8,A,s*21,.3,z);
  u=t=>{dv.forEach((d,i)=>d.arms.forEach((a,j)=>a.rotation.x=-1.3+Math.sin(t*13+i+j*2)*.12));hk.rotation.x=t*.6;hk.rotation.y=t*.9}}
 if(k==2){bx(1.8,.1,5.6,M.dark,s*26,.98,z);bx(.5,.8,4.6,M.dark,s*26,.55,z);bx(.1,3.6,6.4,M.dark,s*32.7,2.3,z);
  const bars=[0,1,2,3,4].map(i=>bx(.1,1,.6,A,s*32.6,1,z-2.4+i*1.2)),pp=[];
  [-1.8,0,1.8].forEach(q=>[-1,1].forEach(r=>{bx(.5,.45,.5,M.dark,s*(26+r*1.5),.4,z+q);pp.push(P(s*(26+r*1.5),z+q,[0x2c3e50,0x7a4a3a,0x3a6a5a,0x4a4a7a,0x6a5a2a,0x2a5a6a][pp.length],-r*f,1))}));
  u=t=>{bars.forEach((b,i)=>{const h=.6+(Math.sin(t*.8+i*1.3)+1)*1.1;b.scale.y=h;b.position.y=.3+h/2});pp.forEach((p,i)=>p.arms[1].rotation.x=-1.1+Math.sin(t*2+i)*.35)}}
 if(k==3){const mp=P(s*24,z,0x2a9d8f,0,0),sq=P(s*31.8,z,0xe9c46a,f,0);
  ad(mp,new THREE.CylinderGeometry(.025,.025,1.5),M.con,0,.8,.55,-.55);ad(mp,new THREE.BoxGeometry(.7,.06,.3),M.warm,0,.12,.95);mp.arms[0].rotation.x=mp.arms[1].rotation.x=-1;
  bx(.1,2.6,5.4,M.glass,s*32.7,2.6,z);bx(.8,.9,1.2,A,s*27,.65,z+3);bx(3,.02,6.8,mat(0xbfefff,.04,.9),s*23,.215,z);
  const bb=[...Array(16)].map(()=>add(new THREE.SphereGeometry(.08,8,6),new THREE.MeshBasicMaterial({color:0xffffff,transparent:true,opacity:.5}),s*(20+Math.random()*8),1,z+(Math.random()-.5)*6));
  u=t=>{mp.position.z=z+Math.sin(t*.7)*2.4;mp.rotation.y=Math.cos(t*.7)>0?0:Math.PI;sq.arms[1].rotation.x=-2.6+Math.sin(t*3)*.3;bb.forEach((b,i)=>b.position.y=.3+((t*.35+i*.19)%1)*3.4)}}
 v.adv=P(s*20,z+(k%2?-2.6:2.6),0x14213d,-f);
 if(k==0){const pw=bx(3,2.2,.05,mat(0x2f6f8f,.7,0),s*22,1.4,z+3.85),pn=P(s*24.5,z+3.2,0x9b59b6,0,0,0xffffff),u0=u;
  add(new THREE.CylinderGeometry(.5,.45,.9,14),A,s*27,.65,z-2.8);bx(.9,.3,.5,M.con,s*28,.35,z+2.2);bx(.9,.3,.5,M.con,s*28,.65,z+2.2);
  [0,1].forEach(i=>add(new THREE.CylinderGeometry(.18,.15,.35,10),mat([0xe63946,0x2a9d8f][i],.6,0),s*21.5,.4,z-3.2+i*.5));
  bx(1.6,.9,1,M.dark,s*18.5,.65,z-2.4);bx(1.3,.02,.8,M.con,s*18.5,1.12,z-2.4);
  u=t=>{u0(t);const q=.15+((t*.25)%1)*.85;pw.scale.x=q;pw.position.x=s*(21+1.5*q);pn.arms[1].rotation.x=-1.5+Math.sin(t*5)*.4}}
 if(k==1){bx(.8,2.2,.8,M.dark,s*32,1.3,z-3.2);for(let i=0;i<5;i++)bx(.82,.05,.82,A,s*32,.6+i*.4,z-3.2);bx(.1,1.8,3,A,s*32.8,3.6,z+.5)}
 if(k==2){const pr=P(s*31.4,z+3.3,0x7a2e4e,-f),u0=u;u=t=>{u0(t);pr.arms[1].rotation.x=-1.8+Math.sin(t*2)*.3}}
 v.upd=u});
/* enseigne BLUVEVA */
const sc=document.createElement('canvas');sc.width=512;sc.height=128;
const sg=sc.getContext('2d'),SGT=new THREE.CanvasTexture(sc);
const sign=()=>{sg.clearRect(0,0,512,128);sg.fillStyle='#e9f2ff';sg.font='300 70px "Cormorant Garamond",serif';
 sg.textAlign='center';sg.textBaseline='middle';if('letterSpacing' in sg)sg.letterSpacing='10px';sg.fillText('BLUVEVA',256,68);SGT.needsUpdate=true};
sign();if(document.fonts)document.fonts.ready.then(sign);
add(new THREE.PlaneGeometry(4.6,1.15),new THREE.MeshBasicMaterial({map:SGT,transparent:true}),0,6.1,8.3);

/* douze plateaux en porte-à-faux + balcons de l’atrium */
for(let i=0;i<12;i++){
 const y=7+i*3.6,ox=Math.sin(i*.9)*2.2,w=24-(i%3)*2;
 bx(w+1,.5,16.6,M.con,ox,y,0);
 bx(w-.4,3.1,15.6,M.win,ox,y+1.8,0);
 bx(w,3.1,16,M.glass,ox,y+1.8,0);
 [-1,1].forEach(s=>{bx(2,.3,12,M.con,s*5,y,-14);bx(.1,.05,12,M.warm,s*4.05,y+.18,-14)});
 bx(12,.3,2,M.con,0,y,-19);bx(10,.05,.1,M.warm,0,y+.18,-18.05);
}
/* atrium : parois de verre, arêtes lumineuses, voile de lumière */
bx(12,.2,12,M.floor,0,.1,-14);
[-1,1].forEach(s=>{bx(.2,50,12,M.glass,s*6,25,-14);bx(.15,50,.15,M.blue,s*5.8,25,-19.8)});
bx(12,50,.2,M.glass,0,25,-20);
add(new THREE.CylinderGeometry(4.5,4.5,50,24,1,true),M.haze,0,25,-14);
/* toit-terrasse */
bx(26,.6,16.6,M.con,0,50.3,0);bx(14,.12,5,M.rpool,0,50.65,2);bx(26,1.1,.1,M.glass,0,51,8.2);

/* ville lointaine et étoiles */
for(let i=0;i<46;i++){const a=Math.random()*6.28,r=140+Math.random()*180,h=25+Math.random()*95,w=14+Math.random()*18;
 bx(w,h,w,M.city,Math.cos(a)*r,h/2,Math.sin(a)*r-20)}
{const a=[];for(let i=0;i<500;i++){const u=Math.random()*6.28,v=.15+Math.random()*.85;a.push(Math.cos(u)*700*(1-v*.3),v*700,Math.sin(u)*700*(1-v*.3))}
 const g=new THREE.BufferGeometry();g.setAttribute('position',new THREE.Float32BufferAttribute(a,3));
 S.add(new THREE.Points(g,new THREE.PointsMaterial({color:0xffffff,size:1.6,sizeAttenuation:false,fog:false})))}

/* éclairage */
S.add(new THREE.HemisphereLight(0x6f8fc7,0x0b0d14,.7));
const sun=new THREE.DirectionalLight(0xffa56b,1.1);sun.position.set(-60,25,90);S.add(sun);
const L1=new THREE.PointLight(0xffc88a,1.4,30);L1.position.set(0,5,0);S.add(L1);
const CL=new THREE.PointLight(0xffe3bd,.9,26);S.add(CL);

/* trajectoire de caméra : [position x,y,z, cible x,y,z] — un point par neuvième du défilement */
const PT=[[-34,4,78,0,18,0],[-14,3.5,54,0,14,0],[0,2.8,28,0,12,0],[0,2.3,10,0,4,-4],[0,2.1,-3,0,3.5,-14],
 [0,2.4,-12,0,6,-14],[0,12,-14,0,30,-18],[0,28,-14,0,50,-18],[0,47,-12,0,52,10],[0,56,-2,0,50,60]];
const V=a=>new THREE.Vector3(...a);PT.length=5;PT[4]=[-2.5,1.9,-.2,-5,1.5,-5.4];
const CP=new THREE.CatmullRomCurve3(PT.map(a=>V(a.slice(0,3))),false,'centripetal'),
      CT=new THREE.CatmullRomCurve3(PT.map(a=>V(a.slice(3))),false,'centripetal');

/* textes : [début, fin, alignement, lieu, titre, texte] */
const C=[
 [-.05,.1,'m h','Visite immersive','BLUVEVA','Une tour de verre et de lumière. Avancez en faisant défiler la page.'],
 [.13,.28,'r','L’approche','La lumière dessine chaque façade','Des plateaux en porte-à-faux, du verre et une pierre claire : la tour se révèle à mesure que l’on s’avance.'],
 [.34,.48,'l','Le hall','Un seuil, puis le silence','Double hauteur, sol sombre et lignes de lumière : l’entrée est pensée comme une scène.'],
 [.54,.68,'r','L’atrium','Un puits de lumière','Un vide central relie tous les niveaux et laisse la verticalité prendre toute la place.'],
 [.71,.84,'l','L’ascension','Douze niveaux, une seule respiration','Chaque balcon ouvre une nouvelle perspective sur l’espace et sur la ville.'],
 [.9,1.05,'m','Le rooftop','La ville à vos pieds','Un bassin suspendu face à l’horizon, au moment où la nuit tombe.','<button class="btn">Demander une visite</button>']];
C.length=3;C[2]=[.72,.92,'l','Le hall','Un seuil, puis le silence','Double hauteur, sol sombre et lignes de lumière : l’entrée est pensée comme une scène.'];
/* visite guidée : accueil, portes, salles */
const sayEl=$('say'),menu=$('menu'),fade=$('fade');
function say(h){if(h){sayEl.innerHTML=h;sayEl.classList.add('on')}else sayEl.classList.remove('on')}
function hall(){mode='hall';hT=T;say('<b>Léa, accueil</b><br>Bienvenue chez BLUVEVA. Où souhaitez-vous aller ? Choisissez un service, j’ouvre la porte.');menu.classList.add('on')}
SV.forEach((v,k)=>{const b=document.createElement('button');b.textContent=v.n;b.onclick=()=>visit(k);menu.appendChild(b)});
function visit(k){const v=SV[k],s=v.sx,z=v.z;cur=k;mode='fly';menu.classList.remove('on');say();document.documentElement.style.overflow='hidden';
 v.g=1;RL.position.set(s*23,5,z);
 tw={t:0,d:6.5,P:new THREE.CatmullRomCurve3([p0.clone(),V([s*7,2.1,z*.8]),V([s*13,2.1,z]),V([s*16,2.2,z])],false,'centripetal'),
  T:new THREE.CatmullRomCurve3([t0.clone(),V([s*13,2.4,z]),V([s*22,2.5,z]),V([s*30,2.4,z])],false,'centripetal'),
  f:()=>{mode='room';v.g=0;rT=T;openShop(k);$('back').classList.add('on')}}}
$('back').onclick=()=>{$('back').classList.remove('on');$('shop').classList.remove('on');say();fade.style.opacity=1;
 setTimeout(()=>{CP.getPoint(1,p0);CT.getPoint(1,t0);cur=-1;document.documentElement.style.overflow='';hall();fade.style.opacity=0},700)};
/* boutique : prestations, vues dans la salle, demande */
const shop=$('shop'),pick=[[],[],[],[]];let rT=0;
const AV=['Marc','Inès','Samir','Julie'];
const OF=[[['Maçonnerie et gros œuvre','Murs, dalles, fondations.'],['Rénovation intérieure','Cloisons, sols, électricité.'],['Peinture et finitions','Murs, plafonds, enduits.'],['Extension','Agrandir sans déménager.']],
 [['Site vitrine','Présenter votre activité en ligne.'],['Boutique en ligne','Vendre et encaisser en ligne.'],['Application mobile','Votre service dans la poche.'],['Maintenance et sécurité','Sauvegardes, mises à jour, assistance.']],
 [['Audit et stratégie','Un état des lieux et un plan d’action.'],['Comptabilité et gestion','Bilans, paie, tableaux de bord.'],['Suivi de projet','Planning, budget, coordination.'],['Formation des équipes','Sur place ou à distance.']],
 [['Bureaux et commerces','Nettoyage quotidien ou hebdomadaire.'],['Vitres et façades','Lavage intérieur et extérieur.'],['Remise en état après travaux','Poussière, peinture, gravats.'],['Contrat d’entretien','Passages réguliers planifiés.']]];
const VW=[[7,-1.8,17,-2.2],[7,1.8,17,2.2],[12,0,19,0],[4,2.5,12,-1.5]];
function view(k,i){const v=SV[k],s=v.sx,z=v.z,q=VW[i];
 tw={t:0,d:2.4,P:new THREE.CatmullRomCurve3([p0.clone(),V([s*(13+q[0]),2.2,z+q[1]])],false,'centripetal'),T:new THREE.CatmullRomCurve3([t0.clone(),V([s*(13+q[2]),1.6,z+q[3]])],false,'centripetal'),f:()=>{}};
 say('<b>'+OF[k][i][0]+'</b><br>'+OF[k][i][1])}
function openShop(k){const v=SV[k];shop.innerHTML='';
 const h=document.createElement('div');h.innerHTML='<h3>'+v.n+'</h3><p>Touchez une prestation pour la voir à l’œuvre. Elle est ajoutée à votre demande ; touchez-la encore pour la retirer.</p>';shop.appendChild(h);
 const go=document.createElement('button'),out=document.createElement('p');go.className='go';go.textContent='Envoyer ma demande';out.style.marginTop='.8rem';
 const upd=()=>{go.disabled=!pick[k].length};
 OF[k].forEach((o,i)=>{const b=document.createElement('button');b.className='o'+(pick[k].includes(i)?' sel':'');b.innerHTML=o[0]+'<small>'+o[1]+'</small>';
  b.onclick=()=>{const j=pick[k].indexOf(i);j<0?pick[k].push(i):pick[k].splice(j,1);b.classList.toggle('sel',j<0);upd();view(k,i)};shop.appendChild(b)});
 go.onclick=()=>{out.textContent='Demande prête : '+pick[k].map(i=>OF[k][i][0]).join(', ')+'. Démonstration : rien n’est envoyé pour l’instant.'};
 shop.append(go,out);upd();shop.classList.add('on');
 say('<b>'+AV[k]+', conseiller</b><br>Bonjour et bienvenue ! Voici notre équipe au travail. Choisissez ce qui vous intéresse.')}
function nav(p){
 dt=Math.min(.05,clk.getDelta());T=clk.elapsedTime;
 if(mode=='walk'){CP.getPoint(sp,p0);CT.getPoint(sp,t0);if(sp>.985&&p>.985)hall()}
 else if(mode=='hall'&&p<.9){mode='walk';say();menu.classList.remove('on')}
 if(tw){tw.t=Math.min(1,tw.t+dt/tw.d);const u=tw.t*tw.t*(3-2*tw.t);tw.P.getPoint(u,p0);tw.T.getPoint(u,t0);if(tw.t>=1){const f=tw.f;tw=null;f()}}
 st+=((mode=='walk'?0:1)-st)*Math.min(1,dt*1.5);
 Sg.position.y=-.2+.4*st;Sg.legs.rotation.x=-1.5*(1-st);
 const wv=mode=='hall'&&T-hT<6,a0=Sg.arms[0],a1=Sg.arms[1];
 a1.rotation.x+=((st<.9?-1.3+Math.sin(T*12)*.08:wv?-2.6+Math.sin(T*7)*.35:.1)-a1.rotation.x)*.12;
 a0.rotation.x+=((st<.9?-1.3+Math.sin(T*11)*.08:.1)-a0.rotation.x)*.12;
 Sg.rotation.y+=((st>.5&&mode=='hall'?Math.atan2(p0.x-Sg.position.x,p0.z-Sg.position.z):0)-Sg.rotation.y)*.06;
 SV.forEach(v=>{v.o+=(v.g-v.o)*Math.min(1,dt*4);v.dp[0].position.z=v.z-.8-v.o*1.6;v.dp[1].position.z=v.z+.8+v.o*1.6;v.upd(T)});
 if(cur>=0){const a=SV[cur].adv,w=T-rT<5&&mode=='room';a.arms[1].rotation.x+=((w?-2.6+Math.sin(T*7)*.35:.1)-a.arms[1].rotation.x)*.12;a.rotation.y+=(Math.atan2(p0.x-a.position.x,p0.z-a.position.z)-a.rotation.y)*.05}
 Sg.sh.position.y=.22-Sg.position.y;
 RL.intensity+=((mode=='room'||(mode=='fly'&&cur>=0)?2.4:0)-RL.intensity)*.08}
const E=C.map(c=>{const d=document.createElement('section');d.className='c '+c[2];
 d.innerHTML=`<small>${c[3]}</small><h2>${c[4]}</h2><p>${c[5]}</p>${c[6]||''}`;$('ch').appendChild(d);return d});

/* boucle de rendu */
let sp=0,mx=0,my=0;const p0=new THREE.Vector3(),t0=new THREE.Vector3(),bar=$('bar').firstChild;
addEventListener('pointermove',e=>{mx=e.clientX/innerWidth-.5;my=e.clientY/innerHeight-.5});
function resize(){R.setSize(innerWidth,innerHeight,false);K.aspect=innerWidth/innerHeight;K.fov=K.aspect<1?72:55;K.updateProjectionMatrix()}
addEventListener('resize',resize);resize();
function tick(){
 const max=document.documentElement.scrollHeight-innerHeight,p=max>0?Math.min(1,Math.max(0,scrollY/max)):0;
 sp+=(p-sp)*.05;
 nav(p);
 K.position.set(p0.x+mx*.6,p0.y-my*.3,p0.z);K.lookAt(t0);CL.position.copy(K.position);
 C.forEach((c,i)=>{const o=Math.max(0,Math.min(1,(sp-c[0])/.03,(c[1]-sp)/.03));
  E[i].style.opacity=o;E[i].style.transform=`translateY(${(1-o)*26}px)`;E[i].classList.toggle('on',o>.8)});
 $('cue').style.opacity=Math.max(0,1-sp*30);bar.style.transform=`scaleX(${sp})`;
 R.render(S,K);requestAnimationFrame(tick)}
tick();
</script>
</body>
</html>
