.textWrapper {
  position: relative;
  padding: 16px;
  margin-bottom: 16px;
  background-color: #d0d0d032;
  border-radius: 6px;
  font-size: 16px;
  line-height: 1.75;
}

.backgroundImage {
  padding-bottom: 5px;
  background-image: linear-gradient(#05c662, #05c662);
  background-size: 0 1px;
  background-position: bottom right;
  background-repeat: no-repeat;
  transition: background-size 0.3s ease-out;
}

.textWrapper:hover .backgroundImage {
  background-size: 100% 1px; /* 幅(100%=文字の長さ) | 高さ(=線の太さ) */
  background-position: bottom left;  /* 左下に配置 */
}
