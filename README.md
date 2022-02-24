# Demo

    private async ETTask CheckHotfix()
    {
        //重新配置热更路径
        AssetComponentConfig.HotfixPath = Application.dataPath + "/../HotfixBundles/";
        
        AssetComponentConfig.DefaultBundlePackageName = "AllBundle";
        List<string> updatePackageBundle = new List<string>(){AssetComponentConfig.DefaultBundlePackageName, "SubBundle"};
        UpdateBundleDataInfo updateBundleDataInfo = await AssetComponent.CheckAllBundlePackageUpdate(updatePackageBundle);
        if (updateBundleDataInfo.NeedUpdate)
        {
            Debug.LogError("需要更新, 大小: " + updateBundleDataInfo.NeedUpdateSize);
            await AssetComponent.DownLoadUpdate(updateBundleDataInfo);
        }
        await AssetComponent.Initialize(AssetComponentConfig.DefaultBundlePackageName);
        await AssetComponent.Initialize("SubBundle");
    }
