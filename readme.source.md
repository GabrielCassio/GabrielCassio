```aura width=860 height=200
<div style={{
  display:'flex', flexdirection:'row',
  width: '100%', height: '100%',
  padding:'15px', gap:'30px',  
  overflow:'hidden',
  borderRadius:'20px',
}}>

  <svg width="860" height="200" style={{position:'absolute', top:'0', left:'0'}}>
    <defs>
      <filter id="blurGlow" x="-50%" y="-50%" width="200%" height="200%">
        <feGaussianBlur stdDeviation="25" />
      </filter>
      <filter id="bgBlurGlow">
        <feGaussianBlur stdDeviation="25" />
      </filter>
      
      {(() => {
        // Elipses
        const elipsePositions = [
          {x: 33, y: -7},
          {x: 33, y: 295},
        ]
        return elipsePositions.map((elp, index) => (
          <radialGradient key={`grad-${index}`} id={`elipseGrad-${index}`} cx="50%" cy="50%" r="70%">
            <stop offset="0%" stopColor="#FF6902" stopOpacity="1" />
            <stop offset="60%" stopColor="#FF6902" stopOpacity="0.5" />
            <stop offset="100%" stopColor="#FF6902" stopOpacity="0" />
          </radialGradient>
        ))
      })()}
    </defs>


    {(() => {
      const elipsePositions = [
        {x: 33, y: -7, w: 330, h: 330},
        {x: 33, y: 295, w: 220, h: 220},
      ]

      return elipsePositions.map((elp, index) => (
        <ellipse
          key={`elipseHalo-${index}`}
          cx={elp.x} cy={elp.y}
          rx={elp.w/2} ry={elp.h/2}
          fill={`url(#elipseGrad-${index})`}
          filter="url(#blurGlow)"
        />
     ));
    })()}
    {(() => {
        // Background Blur
        return (
          <rect key={`blur-bg-card`} width="100%" height="100%" rx="20px" ry="20px" fillOpacity="0.15" stroke="#FFFFFF" strokeOpacity="0.25" strokeWidth="1.5" filter="url(#bgBlurGlow)"/>
        )
      })()}
  </svg>

  <div style={{
    display:'flex', justifyContent:'center', alignItems:'center',
    width:'160px', height:'160px', backgroundColor:'#FD6801',
    borderRadius:'10px'
  }}>
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/images/mascote.svg" width={150} height={150} style={{ objectFit: 'contain' }} />
  </div>
  <div style={{
    display:'flex', flexDirection:'column',
    width:'640px', height:'160px', backgroundColor:'#000000',
    padding:'20px 34px', gap:'35px',
    borderRadius:'10px', 
    fontFamily:'Inter'
  }}>
    <div style={{
      display:'flex', flexDirection:'column', color:'#FFFFFF', gap:'10px'
    }}>
      <span style={{fontWeight:'semi-bold', fontSize:'32px'}}>Gabriel Cassio</span>
      <span style={{fontWeight:'regular', fontSize:'16px' }}>Software Engineering & Architecture</span>
    </div>
    
    <div style={{
      display:'flex', flexDirection:'row',
      gap:'10px'
    }}>
      {(() => {
        const textLabels = ["Full-Stack", "NextJS", "Typescript", "Golang"];
        return textLabels.map((text, index) => (
          <div key={`label-%{index}`}  style={{
            display:'flex', justifyContent:'center', alignItems:'center',
            width:'80px', height:'20px',
            fontSize:'10px', fontWeight:'semi-bold',
            color: '#FFFFFF',
            border: '2px solid #FA6813',
            borderRadius:'30px'
          }}>
            {text}
          </div>
        ));
      })()}
    </div>
  </div>
</div>
```

```aura width=860 height=200
<div style={{
  display:'flex', flexDirection:'row',
  width:'100%', height:'100%', backgroundColor:'#000000', fontFamily:'Inter',
  borderRadius:'20px', overflow:'hidden', position: 'relative'
}}>
  <svg width="860" height="200" style={{ position: 'absolute', top: 0, left: 0 }}>
    <defs>
      <filter id="blurGlow" x="-50%" y="-50%" width="200%" height="200%">
        <feGaussianBlur stdDeviation="25" />
      </filter>
      <radialGradient id="circGrad" cx="50%" cy="50%" r="50%">
        <stop offset="0%" stopColor="#FA6813" stopOpacity="1" />
        <stop offset="60%" stopColor="#FA6813" stopOpacity="0.5" />
        <stop offset="100%" stopColor="#FA6813" stopOpacity="0" />
      </radialGradient>

      {(() => {
        // Create elipses in the card
      })()}

      {(() => {
        // Create lines in the Card
        const linePositions = [281, 579];
        const y1 = 48, y2 = 148;
        const haloWidth = 24, haloBlur = 20;

        return linePositions.flatMap((x, i) => {
          const filterX = x - (haloWidth / 2 + haloBlur * 3);
          const filterY = y1 - haloBlur * 3;
          const filterW = haloWidth + haloBlur * 6;
          const filterH = (y2 - y1) + haloBlur * 6;

          return [
            <linearGradient key={`halo-${i}`} id={`haloGrad${i}`} x1={x} y1={y1} x2={x} y2={y2} gradientUnits="userSpaceOnUse">
              <stop offset="0%" stopColor="#FA6813" stopOpacity="0" />
              <stop offset="50%" stopColor="#FA6813" stopOpacity="0.8" />
              <stop offset="100%" stopColor="#FA6813" stopOpacity="0" />
            </linearGradient>,
            <linearGradient key={`core-${i}`} id={`coreGrad${i}`} x1={x} y1={y1} x2={x} y2={y2} gradientUnits="userSpaceOnUse">
              <stop offset="0%" stopColor="#FFD9B3" stopOpacity="0" />
              <stop offset="50%" stopColor="#FFD9B3" stopOpacity="1" />
              <stop offset="100%" stopColor="#FFD9B3" stopOpacity="0" />
            </linearGradient>,
            <filter key={`filter-${i}`} id={`haloBlur${i}`} filterUnits="userSpaceOnUse" x={filterX} y={filterY} width={filterW} height={filterH}>
              <feGaussianBlur stdDeviation={haloBlur} />
            </filter>,
          ];
        });
      })()}
    </defs>

    <ellipse cx="149" cy="240" rx="120" ry="120" fill="url(#circGrad)" filter="url(#blurGlow)" />
    <ellipse cx="430" cy="240" rx="120" ry="120" fill="url(#circGrad)" filter="url(#blurGlow)" />
    <ellipse cx="711" cy="240" rx="120" ry="120" fill="url(#circGrad)" filter="url(#blurGlow)" />

    {(() => {
      const linePositions = [281, 579];
      const y1 = 48, y2 = 148;
      return linePositions.flatMap((x, i) => [
        <line key={`haloLine-${i}`} x1={x} y1={y1} x2={x} y2={y2} stroke={`url(#haloGrad${i})`} strokeWidth="24" strokeLinecap="round" filter={`url(#haloBlur${i})`}/>,
        <line key={`coreLine-${i}`} x1={x} y1={y1} x2={x} y2={y2} stroke={`url(#coreGrad${i})`} strokeWidth="1.5" strokeLinecap="round"/>,
      ]);
    })()}
  </svg>

  {(() => {
    const stats = [
      { label: 'Repos', value: String(github.stats.totalRepos) },
      { label: 'Stars', value: String(github.stats.totalStars) },
      { label: 'Commits', value: String(github.stats.totalCommits) },
    ]
    return (
      <div style={{
        display:'flex', flexDirection:'row',
        width:'100%', height:'100%', padding:'0px 120px', gap:'190px',
        position: 'relative', zIndex: 1
      }}>
        {stats.map((elem, index) => (
          <div key={index} style={{
            display:'flex', flexDirection:'column', alignItems:'center',
            padding:'52px 0px', gap:'22px', fontWeight: 600
          }}>
            <div style={{ display:'flex', color:'#FD6801', fontSize:'48px' }}>{elem.value}</div>
            <div style={{ display:'flex', color:'#B4B4B4', fontSize:'14px' }}>{elem.label.toUpperCase()}</div>
          </div>
        ))}
      </div>
    )
  })()}
</div>
```

```aura width=860 height=60
<div style={{
  display:'flex',
  width:'100%', height:'100%', backgroundColor:'#EEEEEE', padding:'15px 136px',
  borderRadius:'20px'
}}>
  <div style={{
    display:'flex', flexDirection:'row', gap:'48px'
  }}>
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/docker-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/typescript-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/go-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/nginx-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/python-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/cpp-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/unity-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/react-icn.svg" width={30} height={30} style={{ objectFit: 'cover' }} />
  </div>
</div>

```

```aura width=860 height=256
<div style={{
  display:'flex', flexDirection:'row',
  width:'100%', height:'100%', backgroundColor:'#000000', overflow:'hidden',
  padding:'38px 32px', borderRadius:'20px'
}}>
 <svg width="860" height="256" style={{position:'absolute', top:'0', left:'0'}}>
  <defs>
    <filter id="blurGlow" x="-50%" y="-50%" width="200%" height="200%">
      <feGaussianBlur stdDeviation="25" />
    </filter>

    {(() => {
      const elipsePositions = [
        {x: 2, y: 247},
        {x: 430, y: 128},
        {x: 850, y: 36}
      ];

      return elipsePositions.map((elp, index) => (
        <radialGradient key={`grad-${index}`} id={`elipseGrad-${index}`} cx="50%" cy="50%" r="70%">
          <stop offset="0%" stopColor="#FA6813" stopOpacity="1" />
          <stop offset="60%" stopColor="#FA6813" stopOpacity="0.5" />
          <stop offset="100%" stopColor="#FA6813" stopOpacity="0" />
        </radialGradient>
      ));
    })()}
  </defs>

  {(() => {
    const elipsePositions = [
      {x: 2, y: 247, w: 180, h: 120},
      {x: 430, y: 128, w: 200, h: 200},
      {x: 850, y: 36, w: 180, h:120}
    ];

    return elipsePositions.map((elp, index) => (
      <ellipse
        key={`elipseHalo-${index}`}
        cx={elp.x} cy={elp.y}
        rx={elp.w/2} ry={elp.h/2}
        fill={`url(#elipseGrad-${index})`}
        filter="url(#blurGlow)"
      />
    ));
  })()}
</svg>


  <div style={{
    display:'flex', justifyContent:'center', alignItems:'center',
    overflow:'hidden',
    width:'256px', height:'180px', backgroundColor:'#D9D9D9',
    borderRadius:'20px 0px 0px 20px'
  }}>
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/images/malungo.svg" width={256} height={180} style={{ objectFit:'cover' }} />
    <div style={{position:'absolute', width:'100%', height:'100%', background: 'linear-gradient(235deg, rgba(255, 255, 255, 0) 0%, rgba(25, 17, 11, 0.5) 100%)'}}/>
  </div>
  <div style={{
    display:'flex', justifyContent:'center', alignItems:'center',
    overflow:'hidden',
    width:'256px', height:'180px', backgroundColor:'#D9D9D9',
    margin:'0px 14px'
  }}>
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/images/descin.svg" width={256} height={180} style={{ objectFit: 'cover' }} />
  </div>
  <div style={{
    display:'flex', justifyContent:'center', alignItems:'center',
    overflow:'hidden',
    width:'256px', height:'180px', backgroundColor:'#D9D9D9',
    borderRadius:'0px 20px 20px 0px'
  }}>
    <img src="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/images/cadus.svg" width={256} height={180} style={{ objectFit: 'cover' }} />
    <div style={{position:'absolute', width:'100%', height:'100%', background: 'linear-gradient(45deg,rgba(255, 255, 255, 0) 0%, rgba(25, 17, 11, 0.5) 100%)'}}/>
  </div>
</div>
```


```aura width=170 height=50 link="https://www.linkedin.com/in/gabrielc%C3%A1ssio/" inline align=center
<div style={{
    display: 'flex', width: 150, height: 50,
    fontFamily:'Inter'
  }}>
  <SocialMediaButton
    icon="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/linkedin-icn.svg"
    text="Linkedin"
    textColor="#050003"
    backgroundColor="#FA6813"
    width={150}
    height={50}
    gradientStrokeWidth={0}
    iconSize="30"
  />
</div>
```
```aura width=170 height=50 link="mailto:gcgc@cin.ufpe.br" inline align=center
<div style={{
    display: 'flex', width: 150, height: 50,
    fontFamily:'Inter'
  }}>
  <SocialMediaButton
    icon="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/email-icn.svg"
    text="Email"
    textColor="#050003"
    backgroundColor="#FA6813"
    width={150}
    height={50}
    gradientStrokeWidth={0}
    iconSize="30"
  />
</div>
```
```aura width=170 height=50 link="https://cin.ufpe.br/~gcgc/" inline align=center
<div style={{
    display: 'flex', width: 150, height: 50,
    fontFamily:'Inter'
  }}>
  <SocialMediaButton
    icon="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/portal-icn.svg"
    text="Portal"
    textColor="#050003"
    backgroundColor="#FA6813"
    width={150}
    height={50}
    gradientStrokeWidth={0}
    iconSize="30"
  />
</div>
```
```aura width=170 height=50 link="https://oissac.itch.io/" inline align=center
<div style={{
    display: 'flex', width: 150, height: 50,
    fontFamily:'Inter'
  }}>
  <SocialMediaButton
    icon="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/itch-icn.svg"
    text="Itch.io"
    textColor="#050003"
    backgroundColor="#FA6813"
    width={150}
    height={50}
    gradientStrokeWidth={0}
    iconSize="30"
  />
</div>
```
```aura width=170 height=50 link="https://www.twitch.tv/oissac_cas" inline align=center
<div style={{
    display: 'flex', width: 150, height: 50,
    fontFamily:'Inter'
  }}>
  <SocialMediaButton
    icon="https://raw.githubusercontent.com/GabrielCassio/GabrielCassio/feat/readme-aura-profile/.github/assets/icons/twitch-icn.svg"
    text="Twitch.tv"
    textColor="#050003"
    backgroundColor="#FA6813"
    width={150}
    height={50}
    gradientStrokeWidth={0}
    iconSize="30"
  />
</div>
```