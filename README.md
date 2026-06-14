import { useState, useEffect, useRef } from "react";

const COLORS = {
  bg: "#0d1117",
  surface: "#161b22",
  surfaceHover: "#1c2128",
  border: "#30363d",
  accent: "#58a6ff",
  accentGlow: "#1f6feb",
  green: "#3fb950",
  orange: "#d29922",
  purple: "#bc8cff",
  pink: "#f778ba",
  text: "#e6edf3",
  muted: "#8b949e",
  subtle: "#6e7681",
};

const techStack = {
  Languages: [
    { name: "Python", color: "#3776AB", icon: "🐍" },
    { name: "JavaScript", color: "#F7DF1E", icon: "⚡" },
  ],
  Backend: [
    { name: "FastAPI", color: "#009688", icon: "🚀" },
    { name: "Flask", color: "#ffffff", icon: "🌶️" },
    { name: "Django", color: "#092E20", icon: "🎸" },
  ],
  Frontend: [
    { name: "HTML5", color: "#E34F26", icon: "🌐" },
    { name: "CSS3", color: "#1572B6", icon: "🎨" },
  ],
  Databases: [
    { name: "MySQL", color: "#4479A1", icon: "🗄️" },
    { name: "MongoDB", color: "#47A248", icon: "🍃" },
  ],
  "AI / ML": [
    { name: "PyTorch", color: "#EE4C2C", icon: "🔥" },
    { name: "HuggingFace", color: "#FFD21E", icon: "🤗" },
    { name: "NumPy", color: "#013243", icon: "🔢" },
    { name: "Pandas", color: "#150458", icon: "🐼" },
  ],
  Tools: [
    { name: "Git", color: "#F05032", icon: "🔀" },
    { name: "Postman", color: "#FF6C37", icon: "📬" },
    { name: "VS Code", color: "#007ACC", icon: "💻" },
    { name: "Oracle Cloud", color: "#F80000", icon: "☁️" },
  ],
};

const projects = [
  {
    title: "AI Text Classification App",
    emoji: "🤖",
    desc: "Sentiment analysis using PyTorch & HuggingFace Transformers. Binary classification (positive/negative) with transformer-based models.",
    tags: ["Python", "PyTorch", "HuggingFace", "NLP"],
    date: "May 2026",
    color: "#bc8cff",
  },
  {
    title: "Finance Tracker API",
    emoji: "💰",
    desc: "FastAPI backend with secure RESTful CRUD APIs for managing personal income & expense records. MySQL with proper schema design.",
    tags: ["FastAPI", "MySQL", "REST API", "Python"],
    date: "Apr 2026",
    color: "#3fb950",
  },
  {
    title: "Bug Tracking System",
    emoji: "🐛",
    desc: "Full bug lifecycle management: report, assign, track, and resolve. Priority levels, comments, and a reporting dashboard.",
    tags: ["Full Stack", "Python", "Dashboard"],
    date: "Nov 2025",
    color: "#d29922",
  },
  {
    title: "P2P File Sharing System",
    emoji: "🔗",
    desc: "Decentralized file transfer via socket programming. Supports secure peer-to-peer transfer with connection management.",
    tags: ["Python", "Sockets", "Networking"],
    date: "Oct 2025–2026",
    color: "#58a6ff",
  },
  {
    title: "Student Management System",
    emoji: "🎓",
    desc: "Console-based Python + MySQL app with full CRUD operations, data integrity, and robust input validation.",
    tags: ["Python", "MySQL", "CRUD"],
    date: "Jan 2024",
    color: "#f778ba",
  },
];

const certifications = [
  { name: "Oracle Cloud Infrastructure 2025 – Certified Foundations Associate", issuer: "Oracle", date: "May 2026", icon: "☁️" },
  { name: "Introduction to Software Testing", issuer: "Simplilearn SkillUp", date: "Feb 2026", icon: "🧪" },
  { name: "Code Generation with Generative AI", issuer: "Simplilearn SkillUp", date: "Feb 2026", icon: "⚡" },
  { name: "JavaScript for Beginners", issuer: "Simplilearn SkillUp", date: "May 2026", icon: "🌐" },
  { name: "Computer Vision App with Azure Cognitive Services", issuer: "Microsoft / Coursera", date: "Aug 2025", icon: "👁️" },
  { name: "Prompt Engineering with GitHub Copilot", issuer: "Microsoft & Simplilearn", date: "Nov 2025", icon: "🤖" },
  { name: "Data Structures & Algorithms in Python", issuer: "Simplilearn", date: "Dec 2025", icon: "🐍" },
  { name: "MongoDB Overview: Core Concepts", issuer: "MongoDB, Inc.", date: "Dec 2025", icon: "🍃" },
  { name: "Network Security Associate", issuer: "Fortinet & EduSkills / AICTE", date: "Mar 2024", icon: "🛡️" },
  { name: "Python Programming", issuer: "Reliance Foundation / Skill India", date: "Aug 2025", icon: "💡" },
];

const experience = [
  {
    role: "Python Full Stack Developer Training",
    org: "EduSkills Academy (AICTE)",
    period: "Apr 2026 – Jun 2026",
    points: [
      "Built & deployed web apps using Flask, FastAPI, HTML/CSS/JS frontend",
      "Applied NumPy and Pandas for data handling within real projects",
      "Database design with MySQL and MongoDB",
    ],
    color: COLORS.accent,
    icon: "🎓",
  },
  {
    role: "Cybersecurity Virtual Internship",
    org: "Fortinet & EduSkills (AICTE Supported)",
    period: "Jan 2024 – Mar 2024",
    points: [
      "Worked on simulated threat detection and mitigation scenarios",
      "Completed 10-week Network Security Associate program",
    ],
    color: COLORS.green,
    icon: "🔐",
  },
];

function TypewriterText({ texts, speed = 80, pause = 1800 }) {
  const [display, setDisplay] = useState("");
  const [idx, setIdx] = useState(0);
  const [charIdx, setCharIdx] = useState(0);
  const [deleting, setDeleting] = useState(false);

  useEffect(() => {
    const current = texts[idx];
    const timeout = setTimeout(() => {
      if (!deleting) {
        setDisplay(current.slice(0, charIdx + 1));
        if (charIdx + 1 === current.length) {
          setTimeout(() => setDeleting(true), pause);
        } else {
          setCharIdx((c) => c + 1);
        }
      } else {
        setDisplay(current.slice(0, charIdx - 1));
        if (charIdx - 1 === 0) {
          setDeleting(false);
          setIdx((i) => (i + 1) % texts.length);
          setCharIdx(0);
        } else {
          setCharIdx((c) => c - 1);
        }
      }
    }, deleting ? speed / 2 : speed);
    return () => clearTimeout(timeout);
  }, [charIdx, deleting, idx, texts, speed, pause]);

  return (
    <span>
      {display}
      <span style={{ animation: "blink 1s step-end infinite", color: COLORS.accent }}>|</span>
    </span>
  );
}

function Badge({ name, color, icon }) {
  const [hovered, setHovered] = useState(false);
  return (
    <span
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
      style={{
        display: "inline-flex",
        alignItems: "center",
        gap: 5,
        padding: "4px 12px",
        borderRadius: 20,
        fontSize: 12,
        fontWeight: 600,
        border: `1px solid ${hovered ? color : COLORS.border}`,
        background: hovered ? color + "22" : COLORS.surface,
        color: hovered ? color : COLORS.muted,
        cursor: "default",
        transition: "all 0.2s",
        userSelect: "none",
      }}
    >
      {icon} {name}
    </span>
  );
}

function ProjectCard({ project }) {
  const [hovered, setHovered] = useState(false);
  return (
    <div
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
      style={{
        background: COLORS.surface,
        border: `1px solid ${hovered ? project.color : COLORS.border}`,
        borderRadius: 12,
        padding: "20px 22px",
        cursor: "pointer",
        transition: "all 0.25s",
        transform: hovered ? "translateY(-3px)" : "none",
        boxShadow: hovered ? `0 8px 24px ${project.color}22` : "none",
        position: "relative",
        overflow: "hidden",
      }}
    >
      <div
        style={{
          position: "absolute",
          top: 0, left: 0, right: 0,
          height: 3,
          background: project.color,
          borderRadius: "12px 12px 0 0",
          opacity: hovered ? 1 : 0.3,
          transition: "opacity 0.25s",
        }}
      />
      <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 8 }}>
        <span style={{ fontSize: 22 }}>{project.emoji}</span>
        <span style={{ fontWeight: 700, color: COLORS.text, fontSize: 15 }}>{project.title}</span>
        <span style={{ marginLeft: "auto", fontSize: 11, color: COLORS.subtle }}>{project.date}</span>
      </div>
      <p style={{ color: COLORS.muted, fontSize: 13, lineHeight: 1.6, margin: "0 0 12px" }}>{project.desc}</p>
      <div style={{ display: "flex", flexWrap: "wrap", gap: 6 }}>
        {project.tags.map((t) => (
          <span
            key={t}
            style={{
              fontSize: 11,
              padding: "2px 8px",
              borderRadius: 4,
              background: project.color + "22",
              color: project.color,
              fontWeight: 600,
            }}
          >
            {t}
          </span>
        ))}
      </div>
    </div>
  );
}

function CertCard({ cert }) {
  const [hovered, setHovered] = useState(false);
  return (
    <div
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
      style={{
        display: "flex",
        alignItems: "flex-start",
        gap: 12,
        padding: "14px 16px",
        borderRadius: 10,
        background: hovered ? COLORS.surfaceHover : "transparent",
        border: `1px solid ${hovered ? COLORS.border : "transparent"}`,
        transition: "all 0.2s",
      }}
    >
      <span style={{ fontSize: 20, minWidth: 28 }}>{cert.icon}</span>
      <div style={{ flex: 1 }}>
        <div style={{ fontWeight: 600, color: COLORS.text, fontSize: 13 }}>{cert.name}</div>
        <div style={{ color: COLORS.subtle, fontSize: 12, marginTop: 2 }}>
          {cert.issuer} · {cert.date}
        </div>
      </div>
    </div>
  );
}

function Section({ title, children, icon }) {
  return (
    <div style={{ marginBottom: 40 }}>
      <div
        style={{
          display: "flex",
          alignItems: "center",
          gap: 10,
          marginBottom: 20,
          paddingBottom: 12,
          borderBottom: `1px solid ${COLORS.border}`,
        }}
      >
        <span style={{ fontSize: 18 }}>{icon}</span>
        <h2 style={{ margin: 0, fontSize: 18, fontWeight: 700, color: COLORS.text, fontFamily: "monospace" }}>
          {title}
        </h2>
      </div>
      {children}
    </div>
  );
}

export default function App() {
  const [activeTab, setActiveTab] = useState("overview");

  const tabs = [
    { id: "overview", label: "Overview", icon: "👤" },
    { id: "projects", label: "Projects", icon: "🚀" },
    { id: "skills", label: "Skills", icon: "🛠️" },
    { id: "certs", label: "Certifications", icon: "🏆" },
    { id: "experience", label: "Experience", icon: "💼" },
  ];

  const styles = `
    @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Inter:wght@400;500;600;700&display=swap');
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }
    @keyframes fadeIn { from{opacity:0;transform:translateY(12px)} to{opacity:1;transform:translateY(0)} }
    @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.5} }
    * { box-sizing: border-box; }
    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: #0d1117; }
    ::-webkit-scrollbar-thumb { background: #30363d; border-radius: 3px; }
  `;

  return (
    <div style={{ background: COLORS.bg, minHeight: "100vh", fontFamily: "'Inter', sans-serif", color: COLORS.text }}>
      <style>{styles}</style>

      {/* Hero */}
      <div
        style={{
          background: `linear-gradient(135deg, ${COLORS.bg} 0%, #0f1923 50%, ${COLORS.bg} 100%)`,
          borderBottom: `1px solid ${COLORS.border}`,
          padding: "48px 24px 36px",
          textAlign: "center",
          position: "relative",
          overflow: "hidden",
        }}
      >
        {/* Grid bg decoration */}
        <div style={{
          position: "absolute", inset: 0,
          backgroundImage: `linear-gradient(${COLORS.border}33 1px, transparent 1px), linear-gradient(90deg, ${COLORS.border}33 1px, transparent 1px)`,
          backgroundSize: "40px 40px",
          opacity: 0.4,
        }} />

        {/* Avatar */}
        <div style={{ position: "relative", display: "inline-block", marginBottom: 20 }}>
          <div style={{
            width: 96, height: 96, borderRadius: "50%",
            background: `linear-gradient(135deg, ${COLORS.accentGlow}, ${COLORS.purple})`,
            display: "flex", alignItems: "center", justifyContent: "center",
            fontSize: 42, margin: "0 auto",
            boxShadow: `0 0 32px ${COLORS.accentGlow}66`,
          }}>
            🧑‍💻
          </div>
          <div style={{
            position: "absolute", bottom: 2, right: 2,
            width: 18, height: 18, borderRadius: "50%",
            background: COLORS.green, border: `2px solid ${COLORS.bg}`,
            animation: "pulse 2s ease-in-out infinite",
          }} />
        </div>

        <h1 style={{
          margin: "0 0 8px", fontSize: 32, fontWeight: 800,
          fontFamily: "'JetBrains Mono', monospace",
          background: `linear-gradient(135deg, ${COLORS.text}, ${COLORS.accent})`,
          WebkitBackgroundClip: "text", WebkitTextFillColor: "transparent",
          position: "relative",
        }}>
          Karan Gobade
        </h1>

        <div style={{ fontSize: 16, color: COLORS.accent, fontFamily: "'JetBrains Mono', monospace", marginBottom: 16, position: "relative", minHeight: 24 }}>
          <TypewriterText texts={[
            "Python Developer 🐍",
            "Full Stack Developer 🌐",
            "Software Tester 🧪",
            "API Builder 🚀",
            "ML Enthusiast 🤖",
          ]} />
        </div>

        <p style={{ color: COLORS.muted, maxWidth: 560, margin: "0 auto 24px", fontSize: 14, lineHeight: 1.7, position: "relative" }}>
          IT graduate building production-ready web apps and AI-powered tools.
          Passionate about clean APIs, smart backends, and continuous learning.
        </p>

        {/* Contact badges */}
        <div style={{ display: "flex", flexWrap: "wrap", gap: 10, justifyContent: "center", position: "relative" }}>
          {[
            { label: "📍 Nagpur, MH", color: COLORS.muted },
            { label: "📧 karangobade01@gmail.com", color: COLORS.accent },
            { label: "📱 +91 7057462075", color: COLORS.muted },
          ].map((item) => (
            <span key={item.label} style={{
              padding: "5px 14px", borderRadius: 20, fontSize: 12,
              border: `1px solid ${COLORS.border}`,
              color: item.color, background: COLORS.surface,
            }}>
              {item.label}
            </span>
          ))}
        </div>

        {/* Link buttons */}
        <div style={{ display: "flex", gap: 12, justifyContent: "center", marginTop: 20, flexWrap: "wrap", position: "relative" }}>
          {[
            { label: "🌐 Portfolio", href: "https://karangobade.github.io/portfolio", color: COLORS.accent },
            { label: "💼 LinkedIn", href: "https://linkedin.com/in/karan-gobade", color: "#0A66C2" },
            { label: "🐙 GitHub", href: "https://github.com/karangobade", color: COLORS.text },
          ].map((btn) => (
            <a key={btn.label} href={btn.href} target="_blank" rel="noreferrer" style={{
              padding: "8px 20px", borderRadius: 8, fontSize: 13, fontWeight: 600,
              border: `1px solid ${btn.color}`,
              color: btn.color, background: btn.color + "11",
              textDecoration: "none", transition: "all 0.2s",
            }}>
              {btn.label}
            </a>
          ))}
        </div>
      </div>

      {/* Nav Tabs */}
      <div style={{
        display: "flex", gap: 0, borderBottom: `1px solid ${COLORS.border}`,
        background: COLORS.surface, padding: "0 24px",
        overflowX: "auto",
      }}>
        {tabs.map((tab) => (
          <button
            key={tab.id}
            onClick={() => setActiveTab(tab.id)}
            style={{
              padding: "14px 18px",
              background: "none", border: "none",
              borderBottom: activeTab === tab.id ? `2px solid ${COLORS.accent}` : "2px solid transparent",
              color: activeTab === tab.id ? COLORS.text : COLORS.muted,
              fontWeight: activeTab === tab.id ? 700 : 400,
              fontSize: 13, cursor: "pointer",
              transition: "all 0.2s", whiteSpace: "nowrap",
              fontFamily: "'Inter', sans-serif",
            }}
          >
            {tab.icon} {tab.label}
          </button>
        ))}
      </div>

      {/* Content */}
      <div style={{ maxWidth: 860, margin: "0 auto", padding: "36px 24px", animation: "fadeIn 0.3s ease" }}>

        {/* OVERVIEW */}
        {activeTab === "overview" && (
          <div>
            <Section title="Education" icon="🎓">
              {[
                { degree: "B.Tech – Information Technology", school: "Nagpur Institute of Technology, Nagpur", period: "2023 – 2026", score: null },
                { degree: "Diploma – Computer Science & Engineering", school: "V.A.P. Mahavidyalaya, Almala", period: "2021 – 2023", score: "73%" },
                { degree: "Secondary School (Class X)", school: "Shri Shivaji High School, Latur", period: "2020", score: "80%" },
              ].map((edu, i) => (
                <div key={i} style={{
                  display: "flex", gap: 16, marginBottom: 16,
                  padding: "16px", borderRadius: 10,
                  background: COLORS.surface, border: `1px solid ${COLORS.border}`,
                }}>
                  <div style={{
                    width: 36, height: 36, borderRadius: 8,
                    background: COLORS.accentGlow + "33",
                    display: "flex", alignItems: "center", justifyContent: "center",
                    fontSize: 16, flexShrink: 0,
                  }}>🏛️</div>
                  <div>
                    <div style={{ fontWeight: 700, color: COLORS.text, fontSize: 14 }}>{edu.degree}</div>
                    <div style={{ color: COLORS.muted, fontSize: 13 }}>{edu.school}</div>
                    <div style={{ display: "flex", gap: 12, marginTop: 4 }}>
                      <span style={{ fontSize: 12, color: COLORS.subtle }}>{edu.period}</span>
                      {edu.score && <span style={{ fontSize: 12, color: COLORS.green, fontWeight: 600 }}>Score: {edu.score}</span>}
                    </div>
                  </div>
                </div>
              ))}
            </Section>

            <Section title="Core Competencies" icon="⚡">
              <div style={{ display: "flex", flexWrap: "wrap", gap: 10 }}>
                {[
                  "Python Full Stack Development", "REST API Design & Integration",
                  "Flask · FastAPI · Django", "NumPy & Pandas",
                  "MySQL · MongoDB · DBMS", "Manual Testing & Bug Tracking",
                  "DSA & Problem Solving", "Git & GitHub Version Control",
                  "Socket Programming", "OOP & Algorithms",
                ].map((skill) => (
                  <span key={skill} style={{
                    padding: "6px 14px", borderRadius: 6, fontSize: 13,
                    background: COLORS.accentGlow + "22",
                    color: COLORS.accent, border: `1px solid ${COLORS.accentGlow}44`,
                    fontWeight: 500,
                  }}>{skill}</span>
                ))}
              </div>
            </Section>

            <Section title="GitHub Stats" icon="📊">
              <div style={{ display: "flex", flexDirection: "column", gap: 12, alignItems: "center" }}>
                <img src="https://github-readme-stats.vercel.app/api?username=karangobade&show_icons=true&theme=tokyonight&hide_border=true&bg_color=161b22" alt="GitHub Stats" style={{ borderRadius: 10, maxWidth: "100%" }} />
                <img src="https://streak-stats.demolab.com?user=karangobade&theme=tokyonight&hide_border=true&background=161b22" alt="Streak" style={{ borderRadius: 10, maxWidth: "100%" }} />
                <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=karangobade&layout=compact&theme=tokyonight&hide_border=true&bg_color=161b22" alt="Languages" style={{ borderRadius: 10, maxWidth: "100%" }} />
              </div>
            </Section>
          </div>
        )}

        {/* PROJECTS */}
        {activeTab === "projects" && (
          <Section title="Key Projects" icon="🚀">
            <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(340px, 1fr))", gap: 16 }}>
              {projects.map((p) => <ProjectCard key={p.title} project={p} />)}
            </div>
          </Section>
        )}

        {/* SKILLS */}
        {activeTab === "skills" && (
          <Section title="Tech Stack" icon="🛠️">
            {Object.entries(techStack).map(([category, items]) => (
              <div key={category} style={{ marginBottom: 28 }}>
                <div style={{
                  fontSize: 12, fontWeight: 700, letterSpacing: "0.1em",
                  color: COLORS.subtle, textTransform: "uppercase",
                  marginBottom: 12, fontFamily: "'JetBrains Mono', monospace",
                }}>
                  {category}
                </div>
                <div style={{ display: "flex", flexWrap: "wrap", gap: 8 }}>
                  {items.map((tech) => <Badge key={tech.name} {...tech} />)}
                </div>
              </div>
            ))}
          </Section>
        )}

        {/* CERTIFICATIONS */}
        {activeTab === "certs" && (
          <Section title="Certifications" icon="🏆">
            <div style={{ background: COLORS.surface, borderRadius: 12, border: `1px solid ${COLORS.border}`, overflow: "hidden" }}>
              {certifications.map((cert, i) => (
                <div key={i} style={{ borderBottom: i < certifications.length - 1 ? `1px solid ${COLORS.border}` : "none" }}>
                  <CertCard cert={cert} />
                </div>
              ))}
            </div>
          </Section>
        )}

        {/* EXPERIENCE */}
        {activeTab === "experience" && (
          <Section title="Work Experience" icon="💼">
            {experience.map((exp, i) => (
              <div key={i} style={{
                marginBottom: 24,
                padding: "20px 22px",
                borderRadius: 12,
                background: COLORS.surface,
                border: `1px solid ${COLORS.border}`,
                borderLeft: `3px solid ${exp.color}`,
              }}>
                <div style={{ display: "flex", alignItems: "flex-start", gap: 12, marginBottom: 12 }}>
                  <span style={{ fontSize: 24 }}>{exp.icon}</span>
                  <div>
                    <div style={{ fontWeight: 700, color: COLORS.text, fontSize: 15 }}>{exp.role}</div>
                    <div style={{ color: exp.color, fontSize: 13, fontWeight: 600 }}>{exp.org}</div>
                    <div style={{ color: COLORS.subtle, fontSize: 12, marginTop: 2 }}>{exp.period}</div>
                  </div>
                </div>
                <ul style={{ margin: 0, paddingLeft: 20 }}>
                  {exp.points.map((pt, j) => (
                    <li key={j} style={{ color: COLORS.muted, fontSize: 13, lineHeight: 1.7, marginBottom: 4 }}>{pt}</li>
                  ))}
                </ul>
              </div>
            ))}
          </Section>
        )}
      </div>

      {/* Footer */}
      <div style={{
        textAlign: "center", padding: "20px 24px",
        borderTop: `1px solid ${COLORS.border}`,
        color: COLORS.subtle, fontSize: 12,
        fontFamily: "'JetBrains Mono', monospace",
      }}>
        <span style={{ color: COLORS.accent }}>karangobade</span> · Nagpur, Maharashtra, India · Built with 💙
      </div>
    </div>
  );
}
