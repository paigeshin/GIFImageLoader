# GIFImageLoader

```GIF Image Loader

import SwiftUI
import WebKit

struct GIFImageView: UIViewRepresentable {
    
    private let name: String
    
    init(_ name: String) {
        self.name = name
    }
    
    func makeUIView(context: Context) -> WKWebView {
        let webView: WKWebView = WKWebView()
        guard let url: URL = Bundle.main.url(forResource: name, withExtension: "gif") else {
            print("gif file is not found")
            return webView
        }
        guard let data: Data = try? Data(contentsOf: url) else {
            print("cannot make url")
            return webView
        }
        webView.load(data,
                     mimeType: "image/gif",
                     characterEncodingName: "UTF-8",
                     baseURL: url.deletingLastPathComponent())
        return webView
    }
    
    func updateUIView(_ uiView: WKWebView, context: Context) {
        uiView.reload()
    }
    
}

#if DEBUG
struct GIFImageView_Previews: PreviewProvider {
    static var previews: some View {
        GIFImageView("")
    }
}
#endif


```
