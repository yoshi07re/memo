.Steps > li:not(:last-child)::after {
  position: absolute;
  top: 50%;
  right: -20px;
  display: block;
  width: 10px;
  height: 20px;
  content: "";
  background-color: #09f;
  transform: translate(50%, -50%);
  -webkit-mask-image: url('data:image/svg+xml;charset=UTF-8,<svg xmlns="http://www.w3.org/2000/svg" version="1.1" viewBox="0 0 1 2" preserveAspectRatio="none"><path d="M0,0 L1,1 L0,2 Z"/></svg>');
          mask-image: url('data:image/svg+xml;charset=UTF-8,<svg xmlns="http://www.w3.org/2000/svg" version="1.1" viewBox="0 0 1 2" preserveAspectRatio="none"><path d="M0,0 L1,1 L0,2 Z"/></svg>');
}
