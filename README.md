Demo Tool 程式使用說明
===

## 資料夾說明
-	AISVision_DemoTool : UI相關程式
-	AISVision_DemoTool_Function : model相關程式
-	bin\win64 : 專案使用到的相關dll
-	build\x64 : 專案建置後存放路徑
-	Data : PCB測試照片
-	DITAIModel : anomaly detection訓練的相關檔案
-	model : object/anomaly detection模型

***

## 相機串接說明
-	AISVision_DemoTooll\src\MVVM\Model\CameraModel.cs : 相機指令 (UI端)
-	AISVision_DemoTool_Function\src\Model\Camera.cs : 操控相機運作程式 (model端)

由UI端觸發相機指令後，會在model端執行相機運作的程式

### 範例

### CameraModel.cs

StartCameraFocus()  
{  
&emsp; this.m_cameraIds.StartTrigger();  
}

### Camera.cs

StartTrigger()  
{  
&emsp; m_uCamera.Focus.Trigger();  
}

其中，uEye.Camera內所含為IDS的uEyeDotNet.dll所提供的相機操作相關指令


## 新相機串接方式
1.  安裝新相機驅動
2.	檢查是否uEyeDotNet.dll所提供的相機指令是否能適用，若不能則須新增參考新版相機指令dll
3.	使用該相機適用之dll內的指令，替換掉Camera.cs
    - 如在範例中，僅須替換掉camera.cs中的m_uCamera.Focus.Trigger()
    - 替換後可以在UI測試相機指令是否正常
4.	若程式差異過大，可在model端新增NewCamera.cs，並修改如範例中m_cameraIds.StopTrigger()
    - 範例中StartCameraFocus連結到UI端觸發，更改函數內容即可替成新相機操作
