.accordion-content {
  display: grid;
  grid-template-rows: 0fr;
  transition: grid-template-rows 500ms;
}

.accordion-content[aria-hidden="false"] {
  grid-template-rows: 1fr;
}

.accordion-content > div {
  overflow: hidden;
}

/* other styles */

body {
  font-family: system-ui;
  font-size: 1.25rem;
  line-height: 1.5;
}

.wrapper {
  width: min(65ch, 100% - 4rem);
  margin-inline: auto;
}

.accordion {
  background: #121212;
  color: #effeef;
  padding: 1rem;
}

.accordion-panel {
  padding: 1rem;
  border: 1px solid;
}

.accordion h2 {
  position: relative;
}

.accordion-trigger {
  background: transparent;
  border: 0;
  font: inherit;
  color: inherit;
}

.accordion-trigger::before,
.accordion-trigger::after {
  position: absolute;
  right: 1em;
  content: "";
  display: block;
  width: 1em;
  height: 5px;
  background: currentcolor;
  transition: transform 500ms;
}

.accordion-trigger::after {
  rotate: 90deg;
  translate: 0 -1.5em;
}

.accordion-trigger[aria-expanded="true"]::before,
.accordion-trigger[aria-expanded="true"]::after {
  transform: rotate(45deg);
}
