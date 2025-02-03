body {
  display: grid;
  gap: 1em;
}

@media (min-width: 768px) {
  body {
    grid-template-columns: 1fr 1fr;
  }
  
  h1 {
    align-self: end;
  }
  
  p {
    align-self: start;
  }
  
  img {
    align-self: center;
    grid-column: 2;
    grid-row: 1 / 3;
  }
}

/* Base style */
* {
  margin: 0;
}

h1 {
  background: #fee;
}

p {
  background: #eff;
}

img {
  max-width: 100%;
  height: auto;
}
