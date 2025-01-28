const initializeViewport = () => {
  const debouncedResize = debounce(handleResize);
  window.addEventListener('resize', debouncedResize, false);
  debouncedResize();
};

const handleResize = () => {
  const minWidth = 360;
  const value = window.outerWidth > minWidth ? 'width=device-width,initial-scale=1' : `width=${minWidth}`;
  const viewport = document.querySelector('meta[name="viewport"]');
  if (viewport) {
    if (viewport.getAttribute('content') !== value) {
      viewport.setAttribute('content', value);
    }
  } else {
    console.warn('Viewport meta tag not found!');
  }
};

const debounce = (callback) => {
  let timeout;

  return (...args) => {
    if (timeout !== undefined) cancelAnimationFrame(timeout);
    timeout = requestAnimationFrame(() => callback(...args)); // `this`を削除
  };
};

document.addEventListener("DOMContentLoaded", () => {
  initializeViewport();
});
