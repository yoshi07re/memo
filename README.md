fukidashi-01-03 {
  position: relative;
  width: fit-content;
  padding: 12px 16px;
  border-bottom: 2px solid #333333;
  background-color: #ffffff;
}
.fukidashi-01-03::before {
  content: "";
  position: absolute;
  bottom: -5px;
  left: 50%;
  width: 15px;
  height: 15px;
  box-sizing: border-box;
  background-color: #ffffff; /* 背景色と同じ色を指定 */
  rotate: 135deg;
  translate: -50%;
}
.fukidashi-01-03::after {
  content: "";
  position: absolute;
  bottom: -8px;
  left: 50%;
  z-index: -1;
  width: 15px;
  height: 15px;
  box-sizing: border-box;
  border: 2px solid;
  border-color: #333333 #333333 transparent transparent;
  background-color: #ffffff;
  rotate: 135deg;
  translate: -50%;
}
