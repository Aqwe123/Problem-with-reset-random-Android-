# Problem-with-reset-random-Android-
How i can reset the random without calling again the activity.

so the problem is that when i press the button: New Game the random is going to have the same number of the random, 
and i cant just call again the activity bc i dont want to reset my counter: contador.

how i can just reset my random, so it doesnt always select the same button?

.xml:


    <Button
        android:id="@+id/a1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:layout_marginLeft="28dp"
        android:layout_marginTop="34dp"
        android:text="Button 1" />

    <Button
        android:id="@+id/a2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignLeft="@+id/button1"
        android:layout_below="@+id/button1"
        android:layout_marginTop="23dp"
        android:text="Button 2" />

    <Button
        android:id="@+id/a3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignLeft="@+id/button2"
        android:layout_centerVertical="true"
        android:text="Button 3" />
        
.java:

public class Ejemplo extends Activity implements OnClickListener {
	
	int[] tabla = new int[3];
	Button a1,a2,a3,nuevoJuego;
	int contador = 0;
	
	//int ran=(int)(2*Math.random()) +1;
	
	Random number= new Random();
	int ran=(int) 1+ number.nextInt(2);
	Button[] TablaArray;
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_table_shots);
		
		
		a1= (Button) findViewById(R.id.a1);
		a2= (Button) findViewById(R.id.a2);
		a3= (Button) findViewById(R.id.a3);
		
		nuevoJuego= (Button)findViewById(R.id.nuevoJuego);
		
		//creo el arreglo
		TablaArray = new Button[]{a1,a2,a3};
		
		//con esto ayudo a registrar lo del evento listener
		for(Button b : TablaArray){
			b.setOnClickListener(this);
			
		}
		nuevoJuego.setOnClickListener(new OnClickListener() {
			
			@Override
			public void onClick(View v) {
			
				ran=0; // this is a problem bc it just set my ran in 0 and it doesnt calculate another randon
				
				habilitaydeshabilitarBotones(true);

			}
		});
		
	}
	private void habilitaydeshabilitarBotones(boolean enable){
		//falso para deshabilitar
		for(Button b: TablaArray){
			b.setClickable(enable);
			if(enable){
				//b.setBackgroundColor(Color.BLUE);
				b.setText("");
				
			}
		}
	}

public void gano(){
	
	AlertDialog.Builder dlgAlert = new AlertDialog.Builder(this);
	dlgAlert.setMessage("You just win");
	dlgAlert.setTitle("WIN");
       dlgAlert.setPositiveButton("OK",
               new DialogInterface.OnClickListener() {
                   public void onClick(DialogInterface dialog, int which) {
                       //dismiss the dialog
                   }
               });
       dlgAlert.setCancelable(true);
       dlgAlert.create().show();
	
	a1.setClickable(false);
	a2.setClickable(false);
	a3.setClickable(false);
	
}

	@Override
	public void onClick(View v) {
		
		switch (v.getId()) {
		case R.id.a1:
			if(ran == 1){
				a1.setText("WIN");
				contador= contador + 1;
				gano();
				
			}
			else{
				a1.setText("0");
			}
			a1.setClickable(false);
			break;
			
		case R.id.a2:
			if(ran == 2){
			a2.setText("WIN");
			contador= contador + 1;
			gano();
			}
			else{
				a2.setText("0");
			}
			a2.setClickable(false);
			break;	
			
		case R.id.a3:
			if(ran == 3){
			a3.setText("WIN");
			contador= contador + 1;
			gano();
			}
			else{
				a3.setText("0");
			}
			a3.setClickable(false);
			break;
		}
	}
}

