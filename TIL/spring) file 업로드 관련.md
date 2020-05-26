## spring) file 업로드 관련

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.image.BufferedImage;
import java.io.File;
import java.text.Normalizer;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Map;
import java.util.UUID;

import javax.imageio.ImageIO;

import org.apache.commons.collections.map.CaseInsensitiveMap;
import org.imgscalr.Scalr;
import org.springframework.web.multipart.MultipartFile;

public class FileUtility {

	
	
	
	/**
	 * 파일업로드
	 * @param file 
	 * @param type (지정경로)
	 * @return
	 */
	public static Map file_upload (MultipartFile file, String type) {
		
		CaseInsensitiveMap parameter = new CaseInsensitiveMap();
		
		
		String savePath ="";
		String path_type = type;
		String saveFileName = "";
		String originalfileName = "";
		String file_path = "";
		String genId = UUID.randomUUID().toString();
		Date today = new Date();
        SimpleDateFormat formater = new SimpleDateFormat("yyyyMMdd");
        String date = formater.format(today);


        // 파일 중복명 처리
        // 본래 파일명
        if(file != null){
	    	if(!file.isEmpty()){
	    		String webSavePath1 = "";
	
	    		long fileSize = file.getSize() ;
	        	originalfileName = file.getOriginalFilename();
	        	originalfileName = Normalizer.normalize(originalfileName, Normalizer.Form.NFC); // 자소분리 방지
	            saveFileName = originalfileName;
	            // 저장되는 파일 이름
	            try{
	
	
	            	//운영서버용
	            	String fullpath = "저장될/파일/주소/"+path_type + "/" + date;
	            	String realFilePath = "/" + fullpath;
	
	
	
	            	File dir = new File(realFilePath);
	            	if( !dir.exists() )
	            		dir.mkdirs();
	                savePath = realFilePath + "/" + genId + "_" +saveFileName; // 저장 될 파일 경로
	
	                file.transferTo(new File(savePath)); // 파일 저장
	
	
	                webSavePath1= "/" + fullpath + "/"+ genId + "_" +saveFileName;
	            }
	            catch(Exception e){
	            }
	            
	    		parameter.put("file_path", webSavePath1);
	    		parameter.put("file_org_name", originalfileName);
	    		parameter.put("file_size", fileSize);
	    	}
        }
    	
    	return parameter;
	}
	
	
	
	
	/**
	 * 파일업로드 (이미지인 경우 썸네일 생성)
	 * @param file
	 * @param path
	 * @param file_type
	 * @return
	 */
	public static Map file_upload (MultipartFile file, String path, String file_type) {
		
		CaseInsensitiveMap parameter = new CaseInsensitiveMap();
		
		
		String savePath ="";
		String path_type = path;
		String saveFileName = "";
		String originalfileName = "";
		String file_path = "";
		String genId = UUID.randomUUID().toString();
		Date today = new Date();
        SimpleDateFormat formater = new SimpleDateFormat("yyyyMMdd");
        String date = formater.format(today);
        String fileExt = "";


        // 파일 중복명 처리
        // 본래 파일명
        if(file != null){
	    	if(!file.isEmpty()){
	    		String webSavePath1 = "";
	
	    		long fileSize = file.getSize() ;
	        	originalfileName = file.getOriginalFilename();
	        	originalfileName = Normalizer.normalize(originalfileName, Normalizer.Form.NFC); // 자소분리 방지
	        	fileExt = originalfileName.substring(originalfileName.lastIndexOf(".") + 1);
	            saveFileName = originalfileName;
	            // 저장되는 파일 이름
	            try{
	
	
	            	//운영서버용
	            	String fullpath = "저장될/파일/주소/"+path_type + "/" + date;
	            	String realFilePath = "/" + fullpath;
	
	
	            	File dir = new File(realFilePath);
	            	if( !dir.exists() )
	            		dir.mkdirs();
	            	
	                savePath = realFilePath + "/" + genId + "_" +saveFileName; // 저장 될 파일 경로
	
	                file.transferTo(new File(savePath)); // 파일 저장
	
	
	                webSavePath1= "/" + fullpath + "/"+ genId + "_" +saveFileName;
	            }
	            catch(Exception e){
	            }
	            
	    		parameter.put("file_path", webSavePath1);
	    		parameter.put("file_org_name", originalfileName);
	    		parameter.put("file_size", fileSize);
	    		
	    		
	    		
	    		// 이미지 파일일 경우 썸네일 생성
	    		if ( file_type.equals("image") ) {
	    			try {
						makeThumbnail(webSavePath1);
					} catch (Exception e) {
						e.printStackTrace();
					}
	    		}
	    		
	    		
	    		
	    	}
        }
    	
    	return parameter;
	}
	
	
	
	/**
	 * 썸네일 생성....
	 * @param filePath
	 * @throws Exception
	 */
	private static void makeThumbnail(String filePath) throws Exception { 
		
		File oFile = new File(filePath);

		int index = filePath.lastIndexOf(".");
		String ext = filePath.substring(index + 1); // 파일 확장자

		String tPath = oFile.getParent() + File.separator + "t-" + oFile.getName(); // 썸네일저장 경로
		File tFile = new File(tPath);

		double ratio = 2; // 이미지 축소 비율

		BufferedImage oImage = ImageIO.read(oFile); // 원본이미지
		int tWidth = (int) (oImage.getWidth() / ratio); // 생성할 썸네일이미지의 너비
		int tHeight = (int) (oImage.getHeight() / ratio); // 생성할 썸네일이미지의 높이
		
		BufferedImage tImage = new BufferedImage(tWidth, tHeight, BufferedImage.TYPE_3BYTE_BGR); // 썸네일이미지
		Graphics2D graphic = tImage.createGraphics();
		Image image = oImage.getScaledInstance(tWidth, tHeight, Image.SCALE_SMOOTH);
		graphic.drawImage(image, 0, 0, tWidth, tHeight, null);
		graphic.dispose(); // 리소스를 모두 해제

		ImageIO.write(tImage, ext, tFile);
	}

	
}
```

