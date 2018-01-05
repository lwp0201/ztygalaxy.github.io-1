---
layout: post
title: Android语音识别随时响应
feature-img: "assets/img/pexels/wall_e_thin.jpg"
thumbnail: "assets/img/pexels/wall_e_thin.jpg"
tags: [Android]
---

> 一个语音助手，关键词唤醒总是让人非常头疼. 
>
> 即使两家巨头在各方面都做得不错，在大街上拿起手机向二货一样喊”你好,小娜”“Hey,Siri”,总是让人有点尴尬.理想中的语音助手应该是一个随时随地待命,接收到命令开始执行,不需要的时候保持静默,而不是什么关键词唤醒,然后执行.

**根据目前水平想了一种思路:采声识别，反馈动作完成后通知识别方法继续待命.**

  这里使用科大讯飞提供的SDK作为ASR和TTS引擎,TuringAPI作为机器人反馈源.

**一、Message内容定义**

```java
/** TTS */
public static final int MSG_SPEECH_START = 0;
/** 图灵反馈 */
public static final int MSG_RECOGNIZE_RESULT = 1;
/** ASR*/
public static final int MSG_RECOGNIZE_START = 2;
```

**二、定义一个Handler**

```java
private Handler mHandler = new Handler() {
    public void handleMessage(android.os.Message msg) {
        switch (msg.what) {
            case MSG_SPEECH_START:
                //自定义方法，显示Message于对话框
           setMsg((String) msg.obj,Msg.TYPE_RECEIVED);
                //TTS
           mTtsManager.startTTS((String) msg.obj);
           break;
        case MSG_RECOGNIZE_RESULT:
           setMsg((String) msg.obj,Msg.TYPE_SENT);
                //图灵反馈
           mTuringManager.requestTuring((String) msg.obj);
           break;
        case MSG_RECOGNIZE_START:
                //ASR
           mRecognizerManager.startRecognize();
           break;
      }
     };
};
```

**三、在相关回调中发送Message** 
以TTS回调为例

```java
/**
 * TTS回调
 */
TTSListener myTTSListener = new TTSListener() {
    @Override
    public void onSpeechStart() {
        Log.d(TAG, "onSpeechStart");
    }
    @Override
    public void onSpeechProgressChanged() {}
    @Override
    public void onSpeechPause() {
        Log.d(TAG, "onSpeechPause");
    }
    @Override
    public void onSpeechFinish() {
        Log.d(TAG, "onSpeechFinish");
      mHandler.sendEmptyMessage(MSG_RECOGNIZE_START);
    }
    @Override
    public void onSpeechError(int errorCode) {
        Log.d(TAG, "onSpeechError：" + errorCode);
      mHandler.sendEmptyMessage(MSG_RECOGNIZE_START);
    }
    @Override
    public void onSpeechCancel() {
        Log.d(TAG, "TTS Cancle!");
    }
};
```

**四** 
至此,语音识别就可以随时就位. 
需要注意的是,因为后台运行以及麦克风等,请注意功耗问题,这也是大多数此类应用止步于此的原因.

*需要注意的是,此种方法在人员较多或交流频繁的场合,往往会不断启用并反馈,引起一些不必要操作.因此建议在语句中加入关键词来让App分析对话对象.如:”小炮帮我给老包打电话”,通过语句前置角色或者应用名称等关键词,App收到后拆解分析,确认有关键词后反馈.*

相关：科大讯飞开放平台 Turing机器人