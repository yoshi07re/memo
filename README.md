const initializeViewport = () => {
  const debouncedResize = debounce(handleResize)
  window.addEventListener('resize', debouncedResize, false)
  debouncedResize()
}

const handleResize = () => {
  const minWidth = 360
  const value = window.outerWidth > minWidth ? 'width=device-width,initial-scale=1' : `width=${minWidth}`
  const viewport = document.querySelector('meta[name="viewport"]')
  if (viewport && viewport.getAttribute('content') !== value) {
    viewport.setAttribute('content', value)
  }
}

const debounce = <T extends any[], R>(callback: (...args: T) => R): ((...args: T) => void) => {
  let timeout: number | undefined

  return (...args: T): void => {
    if (timeout !== undefined) cancelAnimationFrame(timeout)
    timeout = requestAnimationFrame(() => callback.apply(this, args))
  }
}

document.addEventListener("DOMContentLoaded", () => {
  initializeViewport()
});
