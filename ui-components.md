# UI Components - Componentes de Interface

## O que e
Padroes e implementacoes de componentes de interface reutilizaveis.

## Design Systems

### Principios
- Consistencia visual
- Reutilizacao de componentes
- Documentacao clara
- Acessibilidade

### Sistemas Populares
- Material Design (Google)
- Ant Design (Alibaba)
- Fluent UI (Microsoft)
- Carbon Design (IBM)
- Chakra UI
- Radix UI

## Componentes Essenciais

### Button
const Button = ({ variant = 'primary', size = 'md', children, ...props }) => {
  const baseClasses = 'rounded font-medium transition-colors';
  
  const variants = {
    primary: 'bg-blue-500 text-white hover:bg-blue-600',
    secondary: 'bg-gray-200 text-gray-800 hover:bg-gray-300',
    danger: 'bg-red-500 text-white hover:bg-red-600'
  };
  
  const sizes = {
    sm: 'px-3 py-1 text-sm',
    md: 'px-4 py-2',
    lg: 'px-6 py-3 text-lg'
  };
  
  return (
    <button
      className={`${baseClasses} ${variants[variant]} ${sizes[size]}`}
      {...props}
    >
      {children}
    </button>
  );
};

### Input
const Input = ({ label, error, ...props }) => {
  return (
    <div className="mb-4">
      {label && (
        <label className="block text-sm font-medium mb-1">
          {label}
        </label>
      )}
      <input
        className={`w-full px-3 py-2 border rounded ${
          error ? 'border-red-500' : 'border-gray-300'
        }`}
        {...props}
      />
      {error && (
        <p className="text-red-500 text-sm mt-1">{error}</p>
      )}
    </div>
  );
};

### Modal
const Modal = ({ isOpen, onClose, title, children }) => {
  if (!isOpen) return null;
  
  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div className="bg-white rounded-lg p-6 max-w-md w-full">
        <div className="flex justify-between items-center mb-4">
          <h2 className="text-xl font-bold">{title}</h2>
          <button onClick={onClose} className="text-gray-500 hover:text-gray-700">
            &times;
          </button>
        </div>
        {children}
      </div>
    </div>
  );
};

### Dropdown
const Dropdown = ({ trigger, items }) => {
  const [isOpen, setIsOpen] = useState(false);
  
  return (
    <div className="relative">
      <button onClick={() => setIsOpen(!isOpen)}>
        {trigger}
      </button>
      {isOpen && (
        <div className="absolute top-full left-0 mt-1 bg-white border rounded shadow-lg">
          {items.map((item, i) => (
            <button
              key={i}
              className="block w-full text-left px-4 py-2 hover:bg-gray-100"
              onClick={() => {
                item.onClick();
                setIsOpen(false);
              }}
            >
              {item.label}
            </button>
          ))}
        </div>
      )}
    </div>
  );
};

### Tabs
const Tabs = ({ tabs }) => {
  const [activeTab, setActiveTab] = useState(0);
  
  return (
    <div>
      <div className="flex border-b">
        {tabs.map((tab, i) => (
          <button
            key={i}
            className={`px-4 py-2 ${
              activeTab === i
                ? 'border-b-2 border-blue-500 text-blue-500'
                : 'text-gray-600'
            }`}
            onClick={() => setActiveTab(i)}
          >
            {tab.label}
          </button>
        ))}
      </div>
      <div className="p-4">
        {tabs[activeTab].content}
      </div>
    </div>
  );
};

## Patterns

### Compound Components
const Select = ({ children, value, onChange }) => {
  return (
    <select value={value} onChange={onChange}>
      {children}
    </select>
  );
};

Select.Option = ({ value, children }) => (
  <option value={value}>{children}</option>
);

// Uso
<Select value={selected} onChange={handleChange}>
  <Select.Option value="1">Option 1</Select.Option>
  <Select.Option value="2">Option 2</Select.Option>
</Select>

### Render Props
const DataList = ({ data, renderItem }) => (
  <ul>
    {data.map((item, i) => (
      <li key={i}>{renderItem(item)}</li>
    ))}
  </ul>
);

// Uso
<DataList
  data={items}
  renderItem={(item) => <span>{item.name}</span>}
/>

### Headless Components
const useToggle = (initial = false) => {
  const [isOpen, setIsOpen] = useState(initial);
  const open = () => setIsOpen(true);
  const close = () => setIsOpen(false);
  const toggle = () => setIsOpen(!isOpen);
  return { isOpen, open, close, toggle };
};

// Uso
function MyComponent() {
  const modal = useToggle();
  return (
    <>
      <button onClick={modal.open}>Open</button>
      {modal.isOpen && <Modal onClose={modal.close} />}
    </>
  );
}

## Acessibilidade

### ARIA Attributes
<button
  aria-label="Close modal"
  aria-expanded={isOpen}
  aria-controls="modal-content"
>
  Close
</button>

### Keyboard Navigation
const handleKeyDown = (e) => {
  if (e.key === 'Enter' || e.key === ' ') {
    e.preventDefault();
    handleClick();
  }
};

### Focus Management
useEffect(() => {
  if (isOpen) {
    inputRef.current?.focus();
  }
}, [isOpen]);

## Bibliotecas Populares

### React
- Chakra UI: chakra-ui.com
- Material-UI: mui.com
- Ant Design: ant.design
- Radix UI: radix-ui.com
- Headless UI: headlessui.com

### Vue
- Vuetify: vuetifyjs.com
- Element Plus: element-plus.org
- PrimeVue: primevue.org

### Web Components
- Lit: lit.dev
- Stencil: stenciljs.com

## Best Practices

### Design
- Seguir design system
- Manter consistencia
- Documentar componentes
- Testar acessibilidade

### Performance
- Lazy load componentes pesados
- Memoizar renders desnecessarios
- Usar virtualizacao para listas grandes

### Manutencao
- Componentizar ao maximo
- Usar TypeScript
- Escrever testes
- Documentar props e uso

## Quando Usar
- Aplicacoes web modernas
- Design systems
- Times grandes
- Projetos de longo prazo