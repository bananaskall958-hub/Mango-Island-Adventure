import React, { useRef, useEffect, useState } from "react";

const SAVE_KEY = "time_survival_save_v4";

export default function TimeSurvivalGame() {
  const canvasRef = useRef(null);

  /* ---------------- SAVE / LOAD ---------------- */

  const loadSave = () => {
    try {
      const data = localStorage.getItem(SAVE_KEY);
      return data ? JSON.parse(data) : null;
    } catch {
      return null;
    }
  };

  const saveGame = (state) => {
    try {
      localStorage.setItem(SAVE_KEY, JSON.stringify(state));
    } catch {}
  };

  const saveData = loadSave();

  /* ---------------- STATE ---------------- */

  const [health, setHealth] = useState(saveData?.health ?? 100);
  const [maxHealth, setMaxHealth] = useState(saveData?.maxHealth ?? 100);
  const [score, setScore] = useState(saveData?.score ?? 0);
  const [gameOver, setGameOver] = useState(false);
  const [level, setLevel] = useState(saveData?.level ?? 1);
  const [day, setDay] = useState(saveData?.day ?? true);

  // Upgrades
  const [weapon, setWeapon] = useState(saveData?.weapon ?? 1);
  const [speedUp, setSpeedUp] = useState(saveData?.speedUp ?? 0);
  const [regen, setRegen] = useState(saveData?.regen ?? 0);
  const [shield, setShield] = useState(saveData?.shield ?? 0);
  const [rapid, setRapid] = useState(saveData?.rapid ?? 0);
  const [bonusDamage, setBonusDamage] = useState(saveData?.bonusDamage ?? 0);

  const [materials, setMaterials] = useState(saveData?.materials ?? 0);

  // Game States
  const [event, setEvent] = useState(null);
  const [eventText, setEventText] = useState("");
  const [homeBase, setHomeBase] = useState(false);
  const [showTutorial, setShowTutorial] = useState(saveData?.tutorialDone ? false : true);

  const allies = useRef([]);

  const player = useRef({
    x: saveData?.x ?? 200,
    y: saveData?.y ?? 200,
    size: 20,
    baseSpeed: 3,
    cooldown: 0,
  });

  const enemies = useRef([]);
  const bullets = useRef([]);
  const boss = useRef(null);
  const keys = useRef({});

  /* ---------------- AUTO SAVE ---------------- */

  useEffect(() => {
    const data = {
      health,
      maxHealth,
      score,
      level,
      day,
      weapon,
      speedUp,
      regen,
      shield,
      rapid,
      bonusDamage,
      materials,
      tutorialDone: !showTutorial,
      x: player.current.x,
      y: player.current.y,
    };

    saveGame(data);
  }, [
    health,
    maxHealth,
    score,
    level,
    day,
    weapon,
    speedUp,
    regen,
    shield,
    rapid,
    bonusDamage,
    materials,
    showTutorial,
  ]);

  /* ---------------- GAME ---------------- */

  useEffect(() => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext("2d");

    /* ---------------- SPAWN ---------------- */

    const spawnEnemy = () => {
      enemies.current.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        size: 18 + level * 2,
        speed: 1 + level * 0.25,
        hp: 25 + level * 6,
      });
    };

    const spawnBoss = () => {
      boss.current = {
        x: canvas.width / 2,
        y: 60,
        size: 55,
        speed: 1.2,
        hp: 400 + level * 120,
        maxHp: 400 + level * 120,
      };
    };

    const spawnAlly = () => {
      allies.current.push({
        x: player.current.x + Math.random() * 40 - 20,
        y: player.current.y + Math.random() * 40 - 20,
        size: 14,
        cooldown: 0,
        level: 1,
      });
    };

    /* ---------------- EVENTS ---------------- */

    const triggerEvent = () => {
      if (Math.random() < 0.5) {
        setEvent("angel");
        const buffs = [
          () => setWeapon((w) => w + 1),
          () => setSpeedUp((s) => s + 1),
          () => setRegen((r) => r + 1),
          () => setShield((s) => s + 1),
          () => setRapid((r) => r + 1),
        ];
        buffs[Math.floor(Math.random() * buffs.length)]();
        setEventText("Angel blessed you ✨");
      } else {
        setEvent("demon");
        setHealth((h) => Math.max(1, h - 10));
        setBonusDamage((d) => d + 0.01);
        setEventText("Demonic crystal absorbed 😈");
      }

      setTimeout(() => {
        setEvent(null);
        setEventText("");
        setHomeBase(true);
      }, 2500);
    };

    /* ---------------- INPUT ---------------- */

    const handleKeyDown = (e) => {
      keys.current[e.key] = true;

      // Tutorial close
      if (showTutorial && e.key === "Enter") {
        setShowTutorial(false);
        return;
      }

      // Home base
      if (homeBase) {
        if (e.key === "n") setHomeBase(false);
        if (e.key === "a" && materials >= 30) {
          setMaterials((m) => m - 30);
          spawnAlly();
        }
        return;
      }

      // Shoot
      if (e.key === " " && player.current.cooldown <= 0 && !event) {
        bullets.current.push({
          x: player.current.x,
          y: player.current.y,
          dy: -7 - rapid,
          dmg: 6 * weapon * (1 + bonusDamage),
        });
        player.current.cooldown = Math.max(5, 25 - rapid * 3);
      }
    };

    const handleKeyUp = (e) => {
      keys.current[e.key] = false;
    };

    /* MOBILE TOUCH */

    const handleTouch = (e) => {
      const t = e.touches[0];
      const rect = canvas.getBoundingClientRect();
      const x = t.clientX - rect.left;
      const y = t.clientY - rect.top;

      player.current.x = x;
      player.current.y = y;

      if (player.current.cooldown <= 0) {
        bullets.current.push({
          x,
          y,
          dy: -7 - rapid,
          dmg: 6 * weapon * (1 + bonusDamage),
        });
        player.current.cooldown = 20;
      }
    };

    canvas.addEventListener("touchmove", handleTouch);
    canvas.addEventListener("touchstart", handleTouch);

    window.addEventListener("keydown", handleKeyDown);
    window.addEventListener("keyup", handleKeyUp);

    /* ---------------- UPDATE ---------------- */

    const update = () => {
      if (gameOver || event || homeBase || showTutorial) return;

      if (regen > 0 && score % 60 === 0) {
        setHealth((h) => Math.min(maxHealth, h + regen));
      }

      player.current.cooldown--;

      const speed = player.current.baseSpeed + speedUp * 0.6;

      if (keys.current["w"]) player.current.y -= speed;
      if (keys.current["s"]) player.current.y += speed;
      if (keys.current["a"]) player.current.x -= speed;
      if (keys.current["d"]) player.current.x += speed;

      /* Allies */
      allies.current.forEach((al) => {
        const dx = player.current.x - al.x;
        const dy = player.current.y - al.y;
        al.x += dx * 0.05;
        al.y += dy * 0.05;

        al.cooldown--;

        if (al.cooldown <= 0 && enemies.current.length) {
          const t = enemies.current[0];
          bullets.current.push({
            x: al.x,
            y: al.y,
            dy: -6,
            dmg: 3 * al.level,
          });
          al.cooldown = 60;
        }
      });

      /* Enemies */
      enemies.current.forEach((enemy) => {
        const dx = player.current.x - enemy.x;
        const dy = player.current.y - enemy.y;
        const dist = Math.hypot(dx, dy);

        enemy.x += (dx / dist) * enemy.speed;
        enemy.y += (dy / dist) * enemy.speed;

        if (dist < enemy.size + player.current.size) {
          setHealth((h) => h - 0.5);
        }
      });

      /* Boss */
      if (boss.current) {
        const dx = player.current.x - boss.current.x;
        const dy = player.current.y - boss.current.y;
        const dist = Math.hypot(dx, dy);

        boss.current.x += (dx / dist) * boss.current.speed;
        boss.current.y += (dy / dist) * boss.current.speed;

        if (dist < boss.current.size + player.current.size) {
          setHealth((h) => h - 1);
        }

        if (boss.current.hp <= 0) {
          boss.current = null;
          setLevel((l) => l + 1);
          setMaterials((m) => m + 40);
          triggerEvent();
        }
      }

      /* Bullets */
      bullets.current.forEach((b) => (b.y += b.dy));

      bullets.current.forEach((b) => {
        enemies.current.forEach((e) => {
          if (Math.hypot(b.x - e.x, b.y - e.y) < e.size) {
            e.hp -= b.dmg;
            b.dead = true;
          }
        });

        if (boss.current) {
          if (Math.hypot(b.x - boss.current.x, b.y - boss.current.y) < boss.current.size) {
            boss.current.hp -= b.dmg;
            b.dead = true;
          }
        }
      });

      enemies.current = enemies.current.filter((e) => {
        if (e.hp <= 0) {
          setMaterials((m) => m + 3);
          return false;
        }
        return true;
      });

      bullets.current = bullets.current.filter((b) => !b.dead && b.y > 0);

      if (score % 1800 === 0 && score > 0 && !boss.current) spawnBoss();

      if (health <= 0) setGameOver(true);

      setScore((s) => s + 1);
    };

    /* ---------------- DRAW ---------------- */

    const draw = () => {
      ctx.clearRect(0, 0, 400, 400);

      /* Tutorial */
      if (showTutorial) {
        ctx.fillStyle = "#000";
        ctx.fillRect(0, 0, 400, 400);

        ctx.fillStyle = "#fff";
        ctx.font = "16px Arial";
        ctx.fillText("WELCOME TIME TRAVELER", 90, 60);
        ctx.font = "12px Arial";
        ctx.fillText("Move: WASD / Touch", 110, 110);
        ctx.fillText("Shoot: Space / Tap", 110, 140);
        ctx.fillText("Survive Cavemen", 130, 170);
        ctx.fillText("Beat Bosses", 135, 200);
        ctx.fillText("Hire Allies at Base (A)", 95, 230);
        ctx.fillText("Press ENTER", 140, 300);
        return;
      }

      /* Home Base */
      if (homeBase) {
        ctx.fillStyle = "#1c1917";
        ctx.fillRect(0, 0, 400, 400);

        ctx.fillStyle = "#fde68a";
        ctx.font = "22px Arial";
        ctx.fillText("HOME BASE", 135, 60);

        ctx.fillStyle = "#fff";
        ctx.font = "13px Arial";
        ctx.fillText("A - Hire Ally (30 Mat)", 100, 120);
        ctx.fillText("N - Next Level", 130, 150);
        ctx.fillText(`Allies: ${allies.current.length}`, 140, 190);
        ctx.fillText(`Materials: ${materials}`, 130, 220);
        return;
      }

      /* World */
      ctx.fillStyle = day ? "#c2b280" : "#0f172a";
      ctx.fillRect(0, 0, 400, 400);

      /* Player */
      ctx.fillStyle = "#2563eb";
      ctx.beginPath();
      ctx.arc(player.current.x, player.current.y, 20, 0, Math.PI * 2);
      ctx.fill();

      /* Allies */
      allies.current.forEach((a) => {
        ctx.fillStyle = "#22c55e";
        ctx.beginPath();
        ctx.arc(a.x, a.y, a.size, 0, Math.PI * 2);
        ctx.fill();
      });

      /* Enemies */
      enemies.current.forEach((e) => {
        ctx.fillStyle = "#7c2d12";
        ctx.beginPath();
        ctx.arc(e.x, e.y, e.size, 0, Math.PI * 2);
        ctx.fill();
      });

      /* Boss */
      if (boss.current) {
        ctx.fillStyle = "#991b1b";
        ctx.beginPath();
        ctx.arc(boss.current.x, boss.current.y, boss.current.size, 0, Math.PI * 2);
        ctx.fill();
      }

      /* Bullets */
      bullets.current.forEach((b) => {
        ctx.fillStyle = "#facc15";
        ctx.beginPath();
        ctx.arc(b.x, b.y, 4, 0, Math.PI * 2);
        ctx.fill();
      });

      /* UI */
      ctx.fillStyle = "#000";
      ctx.font = "12px Arial";
      ctx.fillText(`HP: ${Math.floor(health)}/${maxHealth}`, 10, 16);
      ctx.fillText(`Lvl: ${level}`, 10, 32);
      ctx.fillText(`Mat: ${materials}`, 10, 48);
      ctx.fillText(`Allies: ${allies.current.length}`, 10, 64);

      if (gameOver) {
        ctx.fillStyle = "rgba(0,0,0,0.7)";
        ctx.fillRect(0, 0, 400, 400);
        ctx.fillStyle = "#fff";
        ctx.font = "26px Arial";
        ctx.fillText("YOU DIED", 135, 200);
      }
    };

    /* ---------------- LOOP ---------------- */

    let lastSpawn = 0;

    const loop = (time) => {
      update();
      draw();

      if (time - lastSpawn > 1300 && !event && !homeBase && !showTutorial) {
        spawnEnemy();
        lastSpawn = time;
      }

      requestAnimationFrame(loop);
    };

    requestAnimationFrame(loop);

    return () => {
      window.removeEventListener("keydown", handleKeyDown);
      window.removeEventListener("keyup", handleKeyUp);
      canvas.removeEventListener("touchmove", handleTouch);
      canvas.removeEventListener("touchstart", handleTouch);
    };
  }, [
    health,
    gameOver,
    score,
    level,
    materials,
    weapon,
    day,
    speedUp,
    regen,
    shield,
    rapid,
    maxHealth,
    bonusDamage,
    event,
    homeBase,
    showTutorial,
  ]);

  return (
    <div className="min-h-screen bg-stone-900 flex flex-col items-center justify-center text-white p-4">
      <h1 className="text-3xl font-bold mb-1">⏳ Time Survival: OGA BOGA</h1>
      <p className="mb-2 text-xs text-gray-300 text-center">
        Allies • Tutorial • Mobile Ready
      </p>

      <canvas
        ref={canvasRef}
        width={400}
        height={400}
        className="border-4 border-stone-600 rounded-2xl shadow-lg touch-none"
      />

      <div className="mt-3 text-[11px] text-gray-300 space-y-1 text-center">
        <p>PC: WASD + Space</p>
        <p>Mobile: Drag + Tap</p>
        <p>Base: A=Ally N=Next</p>
      </div>
    </div>
  );
}
