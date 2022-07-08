# addressablesdownloader
# Addressables Downloader

Tải bundle bằng Addressables label. Theo dõi các thông số tải về như kích cỡ gói tải về, tỉ lệ gói tải về, tải thành công chưa, kích cỡ đã tải được.

## Cài đặt

Cài đặt bằng git tag

## Cách dùng
```csharp
private void Awake()
{
    // Khởi tạo download pack
    _downloadPack = new AssetLabelsDownloadPack(assetLabelReference);
}
//Hiển thị cac thông tin của download pack
private void DisplayStatus(AssetsDownloadStatus status)
{
    downloadSizeText.text = $"Size {status.DownloadSizeBytes.ToString()}";
    percentProgressText.text = $"Percent: {status.PercentProgress:F}";
    isDownloadedText.text = $"Is downloaded {status.IsDownloaded}";
    this.statusText.text = $"Status {status.DownloadOperationStatus.ToString()}";
    downloadedBytesText.text = $"Downloaded: {status.DownloadedBytes.ToString()}";
}

//Bắt đầu download
public async UniTask StartDownload()
{
    Debug.Log($"Download started");
    _downloadPack.TrackProgress(Progress.Create<AssetsDownloadStatus>(DisplayStatus));
    var result = await _downloadPack.StartDownloadAsync();
    Debug.Log($"Download completed with result: {result.IsSuccess}, {result.FailureException}");
}
```
