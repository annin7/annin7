private static final int ARRAY_LIST_INITIAL_CAPACITY = 1024;

ArrayList<Particle> particleList;
ParticleObserver currentParticleObserver;

import processing.sound.*;//sound ライブラリーを読み込む
public AudioIn in;//外部音の取得
public Amplitude amp;//

void setup(){//初期設定
  size(640, 640);//紙のサイズ
  frameRate(50f);//読み込む速さ
  
  in = new AudioIn(this, 0);//出力の変数を再定義
  in.start();//読み込みの開始
  amp = new Amplitude(this);//出力の変数の再定義
  amp.input(in);//出力音の中にinの変数を読み込み

  initialize();//関数initializeの出力
}


void draw() {//描画設定
      
  background(255);//背景色
  
  for (Particle currentParticle : particleList) {
    currentParticle.update();
  }
  currentParticleObserver.updateParticleListMembers(particleList);
  for (Particle currentParticle : particleList) {
    currentParticle.display();
  }

}


void initialize() {
  particleList = new ArrayList<Particle>(ARRAY_LIST_INITIAL_CAPACITY);
  currentParticleObserver = new ParticleObserver();

  for (int i = 0; i < 100; i++) {
    MotionLine newMotionLine = new MotionLine(currentParticleObserver, random(0f, width), random(0f, height), random(-10f, 10f), random(-10f, 10f));
    newMotionLine.setColor(color(random(0f, 360f), 100f, 60f));
    currentParticleObserver.addNewParticle(newMotionLine);
  } 
}
