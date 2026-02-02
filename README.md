@charset "utf-8";

/*============================ 
 既存スタイル上書き及び追加
=============================*/
.p-contetns-contact:has(+ .p-contents) {
  padding-bottom: 0;
}

.p-top+.p-contetns-contact {
  padding-top: 32px;
}

.p-contents--top+.p-contents:not(.short-news) {
  margin-top: clamp(64px, calc(32.609865470852014px + 8.370702541106128vw), 120px);
}

.p-contents--top>.p-contetns-contact {
  padding-bottom: 24px;
}

/* メインビジュアル */
.p-top {
  position: relative;
  background-image: url("../images/mv.webp");
  background-position: center;
  background-size: cover;
}

@media screen and (min-width: 768px) {
  .p-top {
    background-color: #f0f0f0;
    border-radius: 15px;
    background-attachment: fixed;
  }
}

@media not screen and (min-width: 768px) {
  .p-top {
    background-color: #000000;
    padding: 130px 0 50px;
    border-radius: 10px;
    background-repeat: no-repeat;
  }
}

/* マップ */
.areamap img {
  display: block;
  margin-inline: auto;
}

.city li a {
  display: grid;
  gap: 16px;
  background-color: #f7f8f8;
  border: solid 5px #658ec3;
  padding: 12px;
}

.city img {
  max-width: 100%;
  width: 100%;
}

.city_name {
  font-size: 1.45rem;
  font-weight: bold;
  margin-bottom: 0.7rem;
  border-bottom: solid 1px black;
}

.city_name span {
  font-size: 1.2rem;
  font-family: "Mrs Saint Delafield", serif;
  font-style: italic;
  font-weight: 100;
  margin-left: 5px;
}

.hotSpot {
  margin-top: 24px;
  width: 100%;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}

.hotSpot__title {
  background-color: #3b5998;
  color: #fff;
  padding: 12px 15px;
  font-weight: bold;
  font-size: 16px;
  letter-spacing: 0.05em;
}

.hotSpot__list {
  list-style: none;
  margin: 0;
  padding: 0;
  background-color: #eef1f6;
}

.hotSpot__list a {
  position: relative;
  padding: 12px 15px;
  text-decoration: none;
  color: #111;
  font-size: 15px;
  border-bottom: 1px dashed #999;
  transition: background-color 0.2s;
  display: flex;
  align-items: center;
}

.hotSpot__list li:last-child a {
  border-bottom: none;
}

.hotSpot__list a:hover {
  background-color: #e0e5ec;
  opacity: 0.9;
}

.hotSpot__list a::before {
  content: '';
  display: block;
  width: 18px;
  height: 18px;
  background-color: #fff;
  border-radius: 50%;
  margin-right: 10px;
  flex-shrink: 0;
}

.hotSpot__list a::after {
  content: '';
  position: absolute;
  left: 22px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 4px 0 4px 6px;
  border-color: transparent transparent transparent #3b5998;
}

@media not (min-width:768px) {
  .city {
    margin-top: 32px;
  }

  .city li:not(:first-of-type) {
    margin-top: 24px;
  }

  .city img {
    width: 100%;
    object-fit: cover;
    aspect-ratio: 16 / 9;
  }
}


@media (min-width:640px) {
  .city li a {
    grid-template-columns: auto 1fr;
  }
}

@media (min-width:768px) {
  /* 1200px以下ではzoomで縮小 */
  #map .inner {
    zoom: min(1, calc(100vw / 1200px));
  }

  .areamap {
    margin-block: 200px;
  }

  .areamap img {
    max-width: 600px;
    padding-right: 40px;
  }

  .city img {
    max-width: 100px;
  }

  .city_name {
    font-size: 1.125rem;
  }

  .city_name span {
    font-size: 1rem;
  }

  .city__detail p:not(.city_name) {
    font-size: 12px;
  }

  .city li {
    position: absolute;
    max-width: 360px;
  }

  .--fukuoka {
    top: -90px;
    left: 430px;
  }

  .--oita {
    top: 40px;
    left: 840px;
  }

  .--kumamoto {
    top: 220px;
    left: 820px;
  }

  .--miyazaki {
    top: 420px;
    left: 770px;
  }

  .--saga {
    top: 20px;
    left: 30px;
  }

  .--nagasaki {
    top: 320px;
    left: 50px;
  }

  .--kagoshima {
    top: 520px;
    left: 70px;
  }

  .hotSpot {
    position: absolute;
    margin-top: 0;
    max-width: 240px;
    top: 600px;
    left: 770px;
  }
}

/* おすすめheading */
.p-issue-item__heading {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding-bottom: 15px;
  font-weight: bold;
}

.issue-n {
  line-height: 1;
  padding: 0 1.5rem;
  border-right: 1px solid #666;
  border-left: 1px solid #666;
  display: inline-block;
  flex-shrink: 0;
  margin-top: -4px;
}

.issue-text {
  flex: 1;
  line-height: 1.3;
  margin-top: -4px;
}
