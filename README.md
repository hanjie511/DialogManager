# DialogManager
Android的对话框工具类，我们可以在我们的项目中建一个公共的对话框工具类，该类主要是用于生成一个带有选择数据功能的对话框。为什么要这样做呢？我们在日常开发中，特别是在
编写录入数据页面时，该页面需要进行大量的数据选择，我们不可能对每一个数据选择项都写一个方法来生成一个数据选择框，这样的做法极大的增加了我们代码的冗余度
，也大大的增加了我们的开发量，使得我们的开发效率变得极其低效。所以，我们可以在我们的项目中添加一个对话框工具类来提高我们的开发效率，降低我们的
代码冗余度。在我们编写项目时，只要我们需要一个数据选择对话框，我们只需要简单的一句调用语句便可以生成一个数据选择框。
## 代码如下
```java
public class DiaLogManager {
   public void showDatePicker(Context context,final String msg) {//通过DatePicker来选择日期的对话框
		Calendar c = Calendar.getInstance();
		int y = c.get(Calendar.YEAR);
		int m = c.get(Calendar.MONTH);
		int d = c.get(Calendar.DAY_OF_MONTH);
		final DatePickerDialog date_dialog = new DatePickerDialog(context, null, y, m, d);
		date_dialog.setButton(DialogInterface.BUTTON_POSITIVE, "确定", new DialogInterface.OnClickListener() {

			@Override
			public void onClick(DialogInterface dialog, int which) {
				// TODO Auto-generated method stub
				 DatePicker picker = date_dialog.getDatePicker();
				 int my_year = picker.getYear();
				 int my_mon = picker.getMonth() + 1;
				 int my_day = picker.getDayOfMonth();
				 String str1 = "";
				 String str2 = "";
				if (my_mon <= 9) {
					str1 = "0" + my_mon;
				} else {
					str1 = "" + my_mon;
				}
				if (my_day <= 9) {
					str2 = "0" + my_day;ri
				} else {
					str2 = "" + my_day;
				}
				String date_str = my_year + "-" + str1 + "-" + str2;//date_str即为选择的日期，日期格式为"YYYY-MM-DD"
				EventBus.getDefault().post(new EventBusTools(msg,date_str));//通过EventBus将选择的数据发送给页面。  
				date_dialog.dismiss();
			}
		});
		date_dialog.setButton(DialogInterface.BUTTON_NEGATIVE, "取消", new DialogInterface.OnClickListener() {

			@Override
			public void onClick(DialogInterface dialog, int which) {
				// TODO Auto-generated method stub
				dialog.dismiss();
			}
		});
		date_dialog.show();
	}
}
```
