
이미지를 웹 URL에서 다운 받은 뒤, 로컬에 저장. 그리고 캐시 메모리에 올린다.

Util 패키지의 것들은 반드시 필요.

꼭 필요한 부분은 

ImageGridFragment.java에서 

private static final String IMAGE_CACHE_DIR = "thumbs"; // 저장할 폴더 지정
private ImageFetcher mImageFetcher; // 선언

mImageThumbSize = getResources().getDimensionPixelSize(R.dimen.image_thumbnail_size);

ImageCache.ImageCacheParams cacheParams =
                new ImageCache.ImageCacheParams(getActivity(), IMAGE_CACHE_DIR);

        cacheParams.setMemCacheSizePercent(0.25f); // Set memory cache to 25% of app memory

        // The ImageFetcher takes care of loading images into our ImageView children asynchronously
        mImageFetcher = new ImageFetcher(getActivity(), mImageThumbSize);
        mImageFetcher.addImageCache(getActivity().getSupportFragmentManager(), cacheParams);
        
        
        Adapter에서 
        
        // Finally load the image asynchronously into the ImageView, this also takes care of
            // setting a placeholder image while the background thread runs
            mImageFetcher.loadImage(Images.imageThumbUrls[position - mNumColumns], imageView);
            해주면 된다.
            
            loadImage(URL, ImageView); 로 사용.
