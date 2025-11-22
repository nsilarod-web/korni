import React, { useState, useRef, useEffect } from 'react';

// --- Icons (Inline Definition to avoid Import Errors) ---
const createIcon = (path) => ({ size = 24, className = "", ...props }) => (
  <svg 
    xmlns="http://www.w3.org/2000/svg" 
    width={size} 
    height={size} 
    viewBox="0 0 24 24" 
    fill="none" 
    stroke="currentColor" 
    strokeWidth="2" 
    strokeLinecap="round" 
    strokeLinejoin="round" 
    className={className}
    {...props}
  >
    {path}
  </svg>
);

const Share2 = createIcon(<><circle cx="18" cy="5" r="3"/><circle cx="6" cy="12" r="3"/><circle cx="18" cy="19" r="3"/><line x1="8.59" y1="13.51" x2="15.42" y2="17.49"/><line x1="15.41" y1="6.51" x2="8.59" y2="10.49"/></>);
const User = createIcon(<><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></>);
const Users = createIcon(<><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></>);
const Plus = createIcon(<><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></>);
const Search = createIcon(<><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></>);
const FileText = createIcon(<><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/><polyline points="10 9 9 9 8 9"/></>);
const Settings = createIcon(<><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"/></>);
const ChevronRight = createIcon(<polyline points="9 18 15 12 9 6"/>);
const Heart = createIcon(<path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>);
const X = createIcon(<><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></>);
const ZoomIn = createIcon(<><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/><line x1="11" y1="8" x2="11" y2="14"/><line x1="8" y1="11" x2="14" y2="11"/></>);
const ZoomOut = createIcon(<><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/><line x1="8" y1="11" x2="14" y2="11"/></>);
const Move = createIcon(<><polyline points="5 9 2 12 5 15"/><polyline points="9 5 12 2 15 5"/><polyline points="15 19 12 22 9 19"/><polyline points="19 9 22 12 19 15"/><line x1="2" y1="12" x2="22" y2="12"/><line x1="12" y1="2" x2="12" y2="22"/></>);
const Trash2 = createIcon(<><polyline points="3 6 5 6 21 6"/><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"/><line x1="10" y1="11" x2="10" y2="17"/><line x1="14" y1="11" x2="14" y2="17"/></>);
const Save = createIcon(<><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></>);
const Home = createIcon(<><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></>);
const Calendar = createIcon(<><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></>);
const Download = createIcon(<><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></>);
const Upload = createIcon(<><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></>);

// --- API Configuration ---
const apiKey = ""; // API key injected by environment

// --- Mock Data & Constants ---
const INITIAL_NODES = [
  { 
    id: 'root', x: 400, y: 300, 
    firstName: 'Иван', lastName: 'Иванов', middleName: 'Иванович', maidenName: '',
    gender: 'male', birthDate: '1990', birthPlace: 'Москва',
    deathDate: '', deathPlace: '', occupation: 'Программист', isAlive: true,
    photo: null, relation: 'self', bio: '', historyContext: '' 
  },
];

// --- Helper Functions ---
const getFullName = (node) => {
  if (!node) return "";
  return `${node.lastName || ''} ${node.firstName || ''} ${node.middleName || ''}`.trim();
};

async function callGemini(prompt) {
  try {
    const response = await fetch(
      `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`,
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          contents: [{ parts: [{ text: prompt }] }],
        }),
      }
    );

    if (!response.ok) {
      throw new Error('Network response was not ok');
    }

    const data = await response.json();
    return data.candidates[0].content.parts[0].text;
  } catch (error) {
    console.error("Gemini API Error:", error);
    return "Извините, сервис временно недоступен. Попробуйте позже.";
  }
}

// --- Custom Spinner (Fixed: Native SVG Animation) ---
const Spinner = ({ size = 18, className = "" }) => (
  <svg 
    xmlns="http://www.w3.org/2000/svg" 
    width={size} 
    height={size} 
    viewBox="0 0 24 24" 
    fill="none" 
    stroke="currentColor" 
    strokeWidth="2" 
    strokeLinecap="round" 
    strokeLinejoin="round" 
    className={className}
  >
    <path d="M21 12a9 9 0 1 1-6.219-8.56" />
    <animateTransform 
      attributeName="transform" 
      attributeType="XML" 
      type="rotate" 
      from="0 12 12" 
      to="360 12 12" 
      dur="1s" 
      repeatCount="indefinite" 
    />
  </svg>
);

// --- UI Components ---

const Button = ({ children, variant = 'primary', className = '', onClick, icon: Icon, title, disabled, loading, component: Component, ...props }) => {
  const baseStyle = "px-4 py-2 rounded-lg font-medium transition-all flex items-center justify-center gap-2 active:scale-95 disabled:opacity-50 disabled:pointer-events-none select-none cursor-pointer";
  const variants = {
    primary: "bg-emerald-600 text-white hover:bg-emerald-700 shadow-md hover:shadow-lg",
    secondary: "bg-white text-slate-700 border border-slate-200 hover:bg-slate-50",
    ghost: "text-slate-600 hover:bg-slate-100",
    danger: "bg-red-50 text-red-600 hover:bg-red-100 border border-red-100",
    magic: "bg-gradient-to-r from-indigo-500 to-purple-600 text-white shadow-md hover:shadow-lg hover:from-indigo-600 hover:to-purple-700"
  };

  const content = (
    <>
      {loading ? <Spinner size={18} /> : Icon && <Icon size={18} />}
      {children}
    </>
  );

  if (Component === 'label') {
    return (
      <label className={`${baseStyle} ${variants[variant]} ${className}`} title={title} {...props}>
        {content}
      </label>
    );
  }

  return (
    <button onClick={onClick} title={title} disabled={disabled || loading} className={`${baseStyle} ${variants[variant]} ${className}`} {...props}>
      {content}
    </button>
  );
};

const Card = ({ children, className = '' }) => (
  <div className={`bg-white rounded-xl shadow-sm border border-slate-100 ${className}`}>
    {children}
  </div>
);

// --- Sub-Pages ---

const LandingPage = ({ onStart }) => (
    <div className="min-h-screen bg-slate-50 font-sans text-slate-800">
      <header className="fixed w-full bg-white/80 backdrop-blur-md z-50 border-b border-slate-200">
        <div className="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
          <div className="flex items-center gap-2 text-emerald-700 font-bold text-xl">
            <Share2 />
            <span className="hidden sm:inline">Семейные корни</span>
          </div>
          <div className="hidden md:flex gap-6 text-sm font-medium text-slate-600">
            <a href="#features" className="hover:text-emerald-600">Возможности</a>
            <a href="#science" className="hover:text-emerald-600">Наука</a>
          </div>
          <Button onClick={onStart} variant="primary">Начать бесплатно</Button>
        </div>
      </header>

      <section className="pt-32 pb-20 px-6">
        <div className="max-w-7xl mx-auto grid md:grid-cols-2 gap-12 items-center">
          <div>
            <h1 className="text-4xl md:text-6xl font-extrabold text-slate-900 leading-tight mb-6">
              Сохрани историю <span className="text-emerald-600">своего рода</span>
            </h1>
            <p className="text-lg text-slate-600 mb-8">
              Интерактивная платформа для создания генеалогического древа. 
              Безопасное хранение данных и <span className="text-purple-600 font-bold inline-flex items-center gap-1"><Search size={16}/> AI-помощник</span>.
            </p>
            <div className="flex flex-col sm:flex-row gap-4">
              <Button onClick={onStart} className="text-lg px-8 py-3">Создать древо</Button>
              <Button variant="secondary" className="text-lg px-8 py-3" icon={Search}>Пример древа</Button>
            </div>
          </div>
          <div className="relative h-[400px] bg-gradient-to-br from-emerald-100 to-teal-50 rounded-3xl overflow-hidden flex items-center justify-center shadow-2xl border border-emerald-200/50">
             <div className="absolute inset-0 opacity-20" style={{backgroundImage: 'radial-gradient(#059669 1px, transparent 1px)', backgroundSize: '20px 20px'}}></div>
             <div className="relative z-10 text-center scale-90 sm:scale-100">
                <div className="w-24 h-24 bg-white rounded-full mx-auto mb-4 shadow-lg flex items-center justify-center border-4 border-emerald-500">
                   <User size={40} className="text-slate-700" />
                </div>
                <div className="w-1 h-16 bg-emerald-400 mx-auto mb-4"></div>
                <div className="flex gap-12 justify-center">
                  <div className="w-16 h-16 bg-white rounded-full shadow-lg flex items-center justify-center border-2 border-blue-400">
                    <User size={24} className="text-slate-400" />
                  </div>
                  <div className="w-16 h-16 bg-white rounded-full shadow-lg flex items-center justify-center border-2 border-pink-400">
                    <User size={24} className="text-slate-400" />
                  </div>
                </div>
             </div>
          </div>
        </div>
      </section>
    </div>
);

const Onboarding = ({ onComplete }) => {
  const [step, setStep] = useState(1);
  const [formData, setFormData] = useState({
    firstName: '', lastName: '', gender: 'male',
    fatherName: '', motherName: ''
  });

  const nextStep = () => {
    if (step === 3) {
      onComplete(formData);
    } else {
      setStep(step + 1);
    }
  };

  return (
    <div className="min-h-screen bg-slate-50 flex items-center justify-center p-6">
      <Card className="w-full max-w-md p-8 relative overflow-hidden">
        <div className="absolute top-0 left-0 w-full h-2 bg-slate-100">
          <div className="h-full bg-emerald-500 transition-all duration-500" style={{width: `${step * 33.3}%`}}></div>
        </div>

        <div className="mb-8 mt-4 text-center">
          <h2 className="text-2xl font-bold text-slate-800">
            {step === 1 && "Давайте знакомиться!"}
            {step === 2 && "Ваши родители"}
            {step === 3 && "Готово!"}
          </h2>
        </div>

        <div className="space-y-4">
          {step === 1 && (
            <>
              <div>
                <label className="block text-sm font-medium text-slate-700 mb-1">Ваше Имя</label>
                <input 
                  type="text" 
                  className="w-full border border-slate-300 rounded-lg p-2 outline-none focus:border-emerald-500"
                  value={formData.firstName}
                  onChange={(e) => setFormData({...formData, firstName: e.target.value})}
                  placeholder="Иван"
                />
              </div>
              <div>
                <label className="block text-sm font-medium text-slate-700 mb-1">Ваша Фамилия</label>
                <input 
                  type="text" 
                  className="w-full border border-slate-300 rounded-lg p-2 outline-none focus:border-emerald-500"
                  value={formData.lastName}
                  onChange={(e) => setFormData({...formData, lastName: e.target.value})}
                  placeholder="Иванов"
                />
              </div>
              <div className="flex gap-4">
                 <button onClick={() => setFormData({...formData, gender: 'male'})} className={`flex-1 p-3 rounded-lg border ${formData.gender === 'male' ? 'border-emerald-500 bg-emerald-50 text-emerald-700' : 'border-slate-200'}`}>Мужской</button>
                 <button onClick={() => setFormData({...formData, gender: 'female'})} className={`flex-1 p-3 rounded-lg border ${formData.gender === 'female' ? 'border-emerald-500 bg-emerald-50 text-emerald-700' : 'border-slate-200'}`}>Женский</button>
              </div>
            </>
          )}

          {step === 2 && (
            <>
              <div>
                <label className="block text-sm font-medium text-slate-700 mb-1">Имя Отца</label>
                <input 
                  type="text" 
                  className="w-full border border-slate-300 rounded-lg p-2 outline-none focus:border-emerald-500"
                  value={formData.fatherName}
                  onChange={(e) => setFormData({...formData, fatherName: e.target.value})}
                  placeholder="Петр"
                />
              </div>
              <div>
                <label className="block text-sm font-medium text-slate-700 mb-1">Имя Матери</label>
                <input 
                  type="text" 
                  className="w-full border border-slate-300 rounded-lg p-2 outline-none focus:border-emerald-500"
                  value={formData.motherName}
                  onChange={(e) => setFormData({...formData, motherName: e.target.value})}
                  placeholder="Мария"
                />
              </div>
            </>
          )}

          {step === 3 && (
             <div className="text-center py-8">
                <div className="w-16 h-16 bg-emerald-100 rounded-full flex items-center justify-center mx-auto mb-4">
                   <Users className="text-emerald-600" size={32} />
                </div>
                <p className="text-slate-600">Базовая информация собрана. Теперь перейдем к самому интересному — вашему древу!</p>
             </div>
          )}

          <Button onClick={nextStep} className="w-full mt-6">
            {step === 3 ? "Перейти в кабинет" : "Далее"} <ChevronRight size={16}/>
          </Button>
        </div>
      </Card>
    </div>
  );
};

// --- Tree Components ---

const NodeCard = ({ node, selected, onClick, onAddRelative, onDragStart }) => {
  const isMale = node.gender === 'male';
  const borderColor = isMale ? 'border-blue-400' : 'border-pink-400';
  const bgColor = isMale ? 'bg-blue-50' : 'bg-pink-50';
  const iconColor = isMale ? 'text-blue-400' : 'text-pink-400';

  const startPos = useRef({ x: 0, y: 0 });

  const handleMouseDown = (e) => {
    e.stopPropagation();
    startPos.current = { x: e.clientX, y: e.clientY }; 
    onDragStart(e, node.id);
  };

  const handleMouseUp = (e) => {
     // Smart click detection: if moved < 5px, treat as click
     const dist = Math.sqrt(
       Math.pow(e.clientX - startPos.current.x, 2) + 
       Math.pow(e.clientY - startPos.current.y, 2)
     );
     if (dist < 5) {
       // Allow event to bubble so parent knows drag ended
       onClick(node.id);
     }
  };

  return (
    <div
      className={`absolute w-48 transition-shadow duration-200 group`}
      style={{ 
        left: node.x, 
        top: node.y,
        zIndex: selected ? 50 : 10,
        cursor: 'grab'
      }}
      onMouseDown={handleMouseDown}
      onMouseUp={handleMouseUp}
      onClick={(e) => e.stopPropagation()} // Stop click bubbling to prevent deselect
    >
      <div className={`relative bg-white rounded-lg shadow-md p-3 border-l-4 ${borderColor} ${selected ? 'ring-2 ring-emerald-500 shadow-xl' : ''}`}>
        
        {/* Buttons */}
        <div className="absolute -top-3 left-1/2 -translate-x-1/2 opacity-0 group-hover:opacity-100 transition-opacity z-20">
          <button title="Добавить родителя" className="bg-slate-700 text-white rounded-full w-6 h-6 flex items-center justify-center hover:bg-emerald-600 shadow-lg hover:scale-110 transition" onClick={(e) => { e.stopPropagation(); onAddRelative(node.id, 'parent'); }}><Plus size={14} /></button>
        </div>
        <div className="absolute -bottom-3 left-1/2 -translate-x-1/2 opacity-0 group-hover:opacity-100 transition-opacity z-20">
           <button title="Добавить ребенка" className="bg-slate-700 text-white rounded-full w-6 h-6 flex items-center justify-center hover:bg-emerald-600 shadow-lg hover:scale-110 transition" onClick={(e) => { e.stopPropagation(); onAddRelative(node.id, 'child'); }}><Plus size={14} /></button>
        </div>
        <div className="absolute top-1/2 -left-3 -translate-y-1/2 opacity-0 group-hover:opacity-100 transition-opacity z-20">
           <button title="Добавить брата/сестру" className="bg-slate-700 text-white rounded-full w-6 h-6 flex items-center justify-center hover:bg-emerald-600 shadow-lg hover:scale-110 transition" onClick={(e) => { e.stopPropagation(); onAddRelative(node.id, 'sibling'); }}><Users size={12} /></button>
        </div>
        <div className="absolute top-1/2 -right-3 -translate-y-1/2 opacity-0 group-hover:opacity-100 transition-opacity z-20">
           <button title="Добавить супруга" className="bg-rose-500 text-white rounded-full w-6 h-6 flex items-center justify-center hover:bg-rose-600 shadow-lg hover:scale-110 transition" onClick={(e) => { e.stopPropagation(); onAddRelative(node.id, 'spouse'); }}><Heart size={12} fill="currentColor" /></button>
        </div>

        <div className="flex items-center gap-3 select-none">
          <div className={`w-10 h-10 ${bgColor} rounded-full flex items-center justify-center ${iconColor} shrink-0`}>
            <User size={20} />
          </div>
          <div className="overflow-hidden w-full">
            <h4 className="font-bold text-slate-800 text-sm truncate leading-tight">
              {node.firstName} {node.lastName}
            </h4>
            {node.maidenName && <p className="text-[10px] text-slate-400 truncate">({node.maidenName})</p>}
            <p className="text-xs text-slate-500 mt-0.5">{node.birthDate || '????'} - {node.isAlive ? '' : (node.deathDate || '...')}</p>
          </div>
        </div>
      </div>
    </div>
  );
};

const ConnectionLine = ({ start, end, type }) => {
  let path;
  
  // Spouse or Sibling horizontal lines
  const isHorizontal = type === 'spouse' || type === 'sibling' || (Math.abs(start.y - end.y) < 50);

  if (isHorizontal) {
      path = `M ${start.x} ${start.y} L ${end.x} ${end.y}`;
  } else {
      const deltaY = end.y - start.y;
      const cp1 = { x: start.x, y: start.y + deltaY / 2 };
      const cp2 = { x: end.x, y: end.y - deltaY / 2 };
      path = `M ${start.x} ${start.y} C ${cp1.x} ${cp1.y}, ${cp2.x} ${cp2.y}, ${end.x} ${end.y}`;
  }

  // Visual styles for different edge types
  let strokeColor = "#94a3b8"; // Default slate
  let strokeWidth = "2";
  let dashArray = "0";

  if (type === 'spouse') {
    strokeColor = "#f43f5e"; // Rose
    strokeWidth = "1.5";
    dashArray = "5,5";
  } else if (type === 'sibling') {
    strokeColor = "#3b82f6"; // Blue
    strokeWidth = "1.5";
    dashArray = "2,4"; // Different dash for siblings
  }

  return <path d={path} fill="none" stroke={strokeColor} strokeWidth={strokeWidth} strokeDasharray={dashArray} className="pointer-events-none" />;
};

// --- Tree Builder Logic ---

const TreeBuilder = ({ nodes, edges, setNodes, setEdges, focusedNodeId, clearFocus }) => {
  const [selectedId, setSelectedId] = useState(null);
  const [transform, setTransform] = useState({ x: 0, y: 0, k: 1 });
  const [isDraggingNode, setIsDraggingNode] = useState(false);
  const [isPanning, setIsPanning] = useState(false);
  const [dragNodeId, setDragNodeId] = useState(null);
  const lastMousePos = useRef({ x: 0, y: 0 });
  const containerRef = useRef(null);
  const [mode, setMode] = useState('canvas');
  const [isImprovingBio, setIsImprovingBio] = useState(false);
  const [isFetchingHistory, setIsFetchingHistory] = useState(false);

  useEffect(() => {
    if (focusedNodeId && mode === 'canvas') {
      const target = nodes.find(n => n.id === focusedNodeId);
      if (target && containerRef.current) {
        const { width, height } = containerRef.current.getBoundingClientRect();
        setTransform({ x: width / 2 - target.x, y: height / 2 - target.y, k: 1 });
        setSelectedId(focusedNodeId);
        clearFocus();
      }
    }
  }, [focusedNodeId, nodes, mode]);

  const handleWheel = (e) => {
    const zoomSensitivity = 0.001;
    const newK = Math.min(Math.max(0.4, transform.k - e.deltaY * zoomSensitivity), 2.5);
    setTransform(prev => ({ ...prev, k: newK }));
  };

  const handleMouseDown = (e) => {
    if (!dragNodeId) {
      setIsPanning(true);
      lastMousePos.current = { x: e.clientX, y: e.clientY };
    }
  };

  const handleNodeDragStart = (e, id) => {
    setIsDraggingNode(true);
    setDragNodeId(id);
    lastMousePos.current = { x: e.clientX, y: e.clientY };
  };

  const handleMouseMove = (e) => {
    const deltaX = e.clientX - lastMousePos.current.x;
    const deltaY = e.clientY - lastMousePos.current.y;
    lastMousePos.current = { x: e.clientX, y: e.clientY };

    if (isDraggingNode && dragNodeId) {
      setNodes(prev => prev.map(n => n.id === dragNodeId ? { ...n, x: n.x + deltaX / transform.k, y: n.y + deltaY / transform.k } : n));
    } else if (isPanning) {
      setTransform(prev => ({ ...prev, x: prev.x + deltaX, y: prev.y + deltaY }));
    }
  };

  const handleMouseUp = (e) => {
    setIsDraggingNode(false);
    setDragNodeId(null);
    setIsPanning(false);
  };

  const handleCanvasClick = (e) => {
      if (!isDraggingNode) {
          setSelectedId(null);
      }
  }

  const addRelative = (sourceId, type) => {
    const sourceNode = nodes.find(n => n.id === sourceId);
    const newId = Date.now().toString();
    let newX = sourceNode.x;
    let newY = sourceNode.y;
    let newLastName = sourceNode.lastName;
    let newBirth = ''; // Keep birth date empty as requested
    
    // --- Logic for Node Placement & Gender ---
    let newGender = sourceNode.gender;
    const sourceEdges = edges.filter(e => e.source === sourceId || e.target === sourceId);

    if (type === 'parent') {
       newY -= 180; 
       newX += (Math.random() * 60 - 30);
       
       // Check if there is already a parent
       const existingParents = edges
         .filter(e => e.target === sourceId && e.type !== 'spouse' && e.type !== 'sibling')
         .map(e => nodes.find(n => n.id === e.source))
         .filter(Boolean);

       if (existingParents.length > 0) {
           // If parent exists, set opposite gender
           newGender = existingParents[0].gender === 'male' ? 'female' : 'male';
           // Try to place next to existing parent
           newX = existingParents[0].x + 220; 
           newY = existingParents[0].y;
       } else {
           newGender = 'male'; // Default first parent to father
       }

    } else if (type === 'child') {
       newY += 180; 
       
       // Spacing for children
       const existingChildren = edges
         .filter(e => e.source === sourceId && e.type !== 'spouse' && e.type !== 'sibling')
         .map(e => nodes.find(n => n.id === e.target))
         .filter(Boolean);
       
       // Offset based on child count to avoid overlap
       const childOffset = existingChildren.length * 150;
       newX = sourceNode.x - 100 + childOffset; 
       
       // Random gender for child
       newGender = Math.random() > 0.5 ? 'male' : 'female';

    } else if (type === 'sibling') {
       newX -= 220; 
       // Random gender for sibling
       newGender = Math.random() > 0.5 ? 'male' : 'female';

    } else if (type === 'spouse') {
       newX += 220; 
       // Opposite gender for spouse
       newGender = sourceNode.gender === 'male' ? 'female' : 'male';
    }

    const newNode = {
      id: newId, x: newX, y: newY,
      firstName: '', lastName: newLastName, middleName: '', maidenName: '',
      gender: newGender, birthDate: newBirth, birthPlace: '',
      deathDate: '', deathPlace: '', occupation: '',
      relation: type, bio: '', historyContext: '', isAlive: true
    };

    setNodes(prev => [...prev, newNode]);
    
    // --- Logic for Edge Creation ---
    let newEdgesList = [];
    
    if (type === 'sibling') {
        // Look for parents of the source
        const parentEdges = edges.filter(e => e.target === sourceId && e.type !== 'spouse' && e.type !== 'sibling');
        
        if (parentEdges.length > 0) {
            // Connect to existing parents
            parentEdges.forEach(pe => newEdgesList.push({ id: `e-${Date.now()}-${pe.source}`, source: pe.source, target: newId }));
        } else {
            // FIX: If no parents, create a direct 'sibling' edge so they are connected visually
            newEdgesList.push({ id: `e-sib-${Date.now()}`, source: sourceId, target: newId, type: 'sibling' });
        }

    } else if (type === 'spouse') {
        newEdgesList.push({ id: `e-${Date.now()}`, source: sourceId, target: newId, type: 'spouse' });

    } else {
        // Parent or Child
        const isParent = type === 'parent';
        // If Parent: new -> source. If Child: source -> new
        newEdgesList.push({ 
            id: `e-${Date.now()}`, 
            source: isParent ? newId : sourceId, 
            target: isParent ? sourceId : newId 
        });
        
        if (isParent) {
            // If adding a parent, check if another parent exists to link them as spouses
            const otherParents = edges
                .filter(e => e.target === sourceId && e.type !== 'spouse' && e.type !== 'sibling')
                .map(e => e.source);
            
            if (otherParents.length > 0) {
                const spouseId = otherParents[0];
                newEdgesList.push({ id: `e-spouse-${Date.now()}`, source: spouseId, target: newId, type: 'spouse' });
            }
        }
    }

    setEdges(prev => [...prev, ...newEdgesList]);
    setSelectedId(newId);
  };

  const deleteNode = (id) => {
     if (id === 'root') return alert("Нельзя удалить корневую персону!");
     setNodes(prev => prev.filter(n => n.id !== id));
     setEdges(prev => prev.filter(e => e.source !== id && e.target !== id));
     setSelectedId(null);
  };

  const selectedNode = nodes.find(n => n.id === selectedId);
  const updateSelectedNode = (field, value) => setNodes(nodes.map(n => n.id === selectedId ? { ...n, [field]: value } : n));

  const improveBio = async () => {
    if (!selectedNode.bio || selectedNode.bio.length < 5) return alert("Напишите пару слов");
    setIsImprovingBio(true);
    const res = await callGemini(`Перепиши художественно на русском: "${selectedNode.bio}"`);
    updateSelectedNode('bio', res);
    setIsImprovingBio(false);
  };

  const getHistoryContext = async () => {
    if (!selectedNode.birthDate) return alert("Нужен год рождения");
    setIsFetchingHistory(true);
    const res = await callGemini(`3 факта о ${selectedNode.birthDate} годе в мире/России. Кратко.`);
    updateSelectedNode('historyContext', res);
    setIsFetchingHistory(false);
  };

  // Logic to find parents for the Inspector view
  const parentIds = selectedNode 
    ? edges
        .filter(e => e.target === selectedNode.id && e.type !== 'spouse')
        .map(e => e.source)
    : [];
  const parents = nodes.filter(n => parentIds.includes(n.id));

  return (
    <div className="flex h-[calc(100vh-64px)] overflow-hidden relative bg-slate-100 select-none">
      <div className="absolute top-4 left-1/2 -translate-x-1/2 z-20 bg-white/90 backdrop-blur rounded-full shadow-lg p-1 flex border border-slate-200">
        <button onClick={() => setMode('canvas')} className={`px-4 py-1.5 rounded-full text-sm font-medium flex items-center gap-2 transition-all ${mode === 'canvas' ? 'bg-emerald-600 text-white shadow' : 'text-slate-500 hover:bg-slate-100'}`}><Share2 size={16}/> Древо</button>
        <button onClick={() => setMode('timeline')} className={`px-4 py-1.5 rounded-full text-sm font-medium flex items-center gap-2 transition-all ${mode === 'timeline' ? 'bg-emerald-600 text-white shadow' : 'text-slate-500 hover:bg-slate-100'}`}><Calendar size={16}/> Лента</button>
      </div>

      {mode === 'canvas' ? (
        <>
          <div className="absolute top-4 left-4 z-20 bg-white p-2 rounded-lg shadow-md flex flex-col gap-2 border border-slate-200">
            <button className="p-2 hover:bg-slate-100 rounded text-slate-600" onClick={() => setTransform(t => ({...t, k: Math.min(t.k + 0.2, 2.5)}))}><ZoomIn size={20}/></button>
            <button className="p-2 hover:bg-slate-100 rounded text-slate-600" onClick={() => setTransform(t => ({...t, k: Math.max(t.k - 0.2, 0.4)}))}><ZoomOut size={20}/></button>
            <div className="h-px bg-slate-200 my-1"></div>
            <button className="p-2 hover:bg-slate-100 rounded text-slate-600" onClick={() => setTransform({x:0, y:0, k:1})}><Move size={20}/></button>
          </div>

          <div 
            ref={containerRef} 
            className="flex-1 relative cursor-default overflow-hidden" 
            onWheel={handleWheel} 
            onMouseDown={handleMouseDown} 
            onMouseMove={handleMouseMove} 
            onMouseUp={handleMouseUp} 
            onMouseLeave={handleMouseUp}
          >
            <div 
                style={{ transform: `translate(${transform.x}px, ${transform.y}px) scale(${transform.k})`, transformOrigin: '0 0', width: '100%', height: '100%', pointerEvents: 'none' }}
            >
              <div 
                className="absolute inset-0 w-full h-full pointer-events-auto"
                onClick={handleCanvasClick} // Handle background click
              >
                  <svg className="absolute top-0 left-0 w-[5000px] h-[5000px] pointer-events-none overflow-visible">
                    {edges.map(edge => {
                      const s = nodes.find(n => n.id === edge.source);
                      const t = nodes.find(n => n.id === edge.target);
                      if (!s || !t) return null;
                      
                      const type = edge.type; // Pass type to component
                      let start, end;
                      const isHorizontal = type === 'spouse' || type === 'sibling' || (Math.abs(s.y - t.y) < 50);

                      if (isHorizontal) {
                          const leftNode = s.x < t.x ? s : t;
                          const rightNode = s.x < t.x ? t : s;
                          start = { x: leftNode.x + 192, y: leftNode.y + 40 };
                          end = { x: rightNode.x, y: rightNode.y + 40 };
                      } else {
                          start = { x: s.x + 96, y: s.y + 70 };
                          end = { x: t.x + 96, y: t.y };
                      }
                      return <ConnectionLine key={edge.id} start={start} end={end} type={type} />
                    })}
                  </svg>
                  {nodes.map(node => (
                    <NodeCard key={node.id} node={node} selected={selectedId === node.id} onClick={setSelectedId} onAddRelative={addRelative} onDragStart={handleNodeDragStart} />
                  ))}
              </div>
            </div>
          </div>
        </>
      ) : (
        <div className="flex-1 overflow-y-auto bg-slate-50">
           <div className="p-8 max-w-3xl mx-auto">
               <div className="relative border-l-4 border-emerald-200 ml-4 space-y-8 pb-12">
                  {[...nodes]
                    .filter(n => n.birthDate && !isNaN(parseInt(n.birthDate)))
                    .sort((a,b) => parseInt(a.birthDate) - parseInt(b.birthDate))
                    .map((node) => (
                      <div key={node.id} className="relative pl-8">
                         <div className="absolute -left-[13px] top-1 w-6 h-6 rounded-full bg-white border-4 border-emerald-500"></div>
                         <div className="bg-white p-4 rounded-xl shadow-sm border border-slate-100 flex justify-between">
                            <div><h3 className="font-bold text-slate-800">{getFullName(node)}</h3><span className="text-sm text-emerald-600 font-bold">{node.birthDate}</span></div>
                         </div>
                      </div>
                  ))}
               </div>
           </div>
        </div>
      )}

      {mode === 'canvas' && (
        <div className={`fixed md:relative inset-y-0 right-0 w-80 md:w-96 bg-white shadow-2xl md:shadow-xl border-l border-slate-200 flex flex-col transition-transform duration-300 z-40 transform ${selectedId ? 'translate-x-0' : 'translate-x-full md:mr-[-24rem]'}`}>
            {selectedNode && (
               <>
                <div className="p-4 border-b flex justify-between items-center bg-slate-50">
                   <h3 className="font-bold text-slate-700">Карточка персоны</h3>
                   <button onClick={() => setSelectedId(null)} className="text-slate-400 hover:text-slate-600 p-1 hover:bg-slate-200 rounded"><X size={20}/></button>
                </div>
                <div className="p-4 overflow-y-auto flex-1 space-y-6">
                   <div className="text-center">
                      <div className="w-24 h-24 bg-slate-100 border-2 border-dashed border-slate-300 rounded-full mx-auto mb-2 flex items-center justify-center cursor-pointer hover:border-emerald-500 transition-colors">
                         {selectedNode.photo ? <img src={selectedNode.photo} className="w-full h-full rounded-full object-cover"/> : <User size={40} className="text-slate-300"/>}
                      </div>
                   </div>

                   <div className="space-y-4">
                      {/* 1. Name Fields */}
                      <div className="grid grid-cols-1 gap-3">
                         <div>
                            <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Фамилия</label>
                            <input className="w-full border border-slate-300 p-2 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.lastName} onChange={(e) => updateSelectedNode('lastName', e.target.value)}/>
                         </div>
                         <div className="grid grid-cols-2 gap-2">
                            <div>
                                <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Имя</label>
                                <input className="w-full border border-slate-300 p-2 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.firstName} onChange={(e) => updateSelectedNode('firstName', e.target.value)}/>
                            </div>
                            <div>
                                <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Отчество</label>
                                <input className="w-full border border-slate-300 p-2 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.middleName} onChange={(e) => updateSelectedNode('middleName', e.target.value)}/>
                            </div>
                         </div>
                         {selectedNode.gender === 'female' && (
                             <div>
                                <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Девичья фамилия</label>
                                <input className="w-full border border-slate-300 p-2 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.maidenName} onChange={(e) => updateSelectedNode('maidenName', e.target.value)}/>
                             </div>
                         )}
                         <div>
                            <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Пол</label>
                            <select className="w-full border border-slate-300 p-2 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.gender} onChange={(e) => updateSelectedNode('gender', e.target.value)}>
                               <option value="male">Мужской</option>
                               <option value="female">Женский</option>
                            </select>
                         </div>
                      </div>

                      <div className="h-px bg-slate-200 my-2"></div>

                      {/* 2. Birth Date & Place */}
                      <div className="space-y-3">
                        <div>
                            <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Дата рождения</label>
                            <input className="w-full border border-slate-300 p-2 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" placeholder="ГГГГ" value={selectedNode.birthDate} onChange={(e) => updateSelectedNode('birthDate', e.target.value)}/>
                        </div>
                        <div>
                            <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Место рождения</label>
                            <div className="relative">
                                <input className="w-full border border-slate-300 p-2 pl-8 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.birthPlace} onChange={(e) => updateSelectedNode('birthPlace', e.target.value)}/>
                                <Home size={14} className="absolute left-2.5 top-2.5 text-slate-400"/>
                            </div>
                        </div>
                        <div className="mt-1">
                            <Button variant="secondary" className="w-full text-xs flex justify-between border-purple-200 hover:border-purple-400 hover:bg-purple-50 text-purple-700" icon={Search} onClick={getHistoryContext} loading={isFetchingHistory}>
                              Исторический контекст
                            </Button>
                            {selectedNode.historyContext && <div className="mt-2 p-3 bg-purple-50 border border-purple-100 rounded-lg text-xs text-slate-700 italic">{selectedNode.historyContext}</div>}
                        </div>
                      </div>

                      {/* 3. Is Alive Checkbox */}
                      <div className="flex items-center gap-2 bg-emerald-50 p-2 rounded-lg border border-emerald-100 mt-2">
                          <input 
                            type="checkbox" 
                            id="isAlive" 
                            className="w-4 h-4 text-emerald-600 rounded focus:ring-emerald-500"
                            checked={selectedNode.isAlive !== false} // Default to true if undefined
                            onChange={(e) => updateSelectedNode('isAlive', e.target.checked)}
                          />
                          <label htmlFor="isAlive" className="text-sm font-medium text-emerald-800">Человек жив</label>
                      </div>

                      {/* 4. Death Date & Place (Conditional) */}
                      {!selectedNode.isAlive && (
                          <div className="space-y-3">
                             <div>
                                <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Дата смерти</label>
                                <input className="w-full border border-slate-300 p-2 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" placeholder="—" value={selectedNode.deathDate} onChange={(e) => updateSelectedNode('deathDate', e.target.value)}/>
                             </div>
                             <div>
                                <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Место смерти</label>
                                <div className="relative">
                                    <input className="w-full border border-slate-300 p-2 pl-8 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.deathPlace} onChange={(e) => updateSelectedNode('deathPlace', e.target.value)}/>
                                    <Home size={14} className="absolute left-2.5 top-2.5 text-slate-400"/>
                                </div>
                             </div>
                          </div>
                      )}

                      <div className="h-px bg-slate-200 my-2"></div>

                      {/* 5. Lower Fields (Occupation) */}
                      <div>
                        <label className="text-xs font-bold text-slate-500 uppercase tracking-wider block mb-1">Профессия</label>
                        <div className="relative">
                            <input className="w-full border border-slate-300 p-2 pl-8 rounded-lg text-sm focus:ring-2 focus:ring-emerald-500 outline-none" value={selectedNode.occupation} onChange={(e) => updateSelectedNode('occupation', e.target.value)}/>
                            <FileText size={14} className="absolute left-2.5 top-2.5 text-slate-400"/>
                        </div>
                      </div>

                      {/* 7. Biography (Moved UP) */}
                      <div className="border-t border-slate-100 pt-4">
                          <div className="flex justify-between items-center mb-2">
                            <h4 className="font-bold text-sm text-slate-700 flex items-center gap-2"><FileText size={14}/> Биография</h4>
                            <Button variant="magic" className="px-2 py-1 text-xs h-7" icon={Search} onClick={improveBio} loading={isImprovingBio}>Улучшить</Button>
                          </div>
                          <textarea className="w-full border border-slate-300 rounded-lg p-2 text-sm h-32 focus:ring-2 focus:ring-emerald-500 outline-none resize-none" value={selectedNode.bio || ''} onChange={(e) => updateSelectedNode('bio', e.target.value)}></textarea>
                       </div>

                      {/* 6. Parents Links (Moved DOWN) */}
                      {parents.length > 0 && (
                          <div className="mt-2 p-3 bg-slate-50 rounded-lg border border-slate-100">
                             <span className="text-xs font-bold text-slate-500 block mb-2">Родители</span>
                             <div className="flex flex-wrap gap-2">
                                 {parents.map(p => (
                                     <button 
                                       key={p.id} 
                                       onClick={() => setSelectedId(p.id)}
                                       className="text-xs bg-white border hover:border-emerald-400 text-slate-700 px-2 py-1 rounded flex items-center gap-1 transition-colors shadow-sm"
                                     >
                                         <User size={10} /> {getFullName(p)}
                                     </button>
                                 ))}
                             </div>
                          </div>
                      )}
                   </div>
                </div>
                <div className="p-4 border-t bg-slate-50 space-y-2">
                   <Button className="w-full" icon={Save} onClick={() => setSelectedId(null)}>Сохранить</Button>
                   <Button className="w-full" variant="danger" icon={Trash2} onClick={() => deleteNode(selectedId)}>Удалить</Button>
                </div>
               </>
            )}
        </div>
      )}
    </div>
  );
}
