using ZO.Modul1;

 private void button1_Click(object sender, EventArgs e)
 {
     String login_user = Login_TexBox.Text;
     string passwor_user = Password_TextBox.Text;


     Users acker = null;
     int role;
     using (Model1 db = new Model1())
     {
         acker = db.Users.Where(b => b.Login == login_user && b.Password == passwor_user).FirstOrDefault();
         role = Convert.ToInt32(acker.id_role);
     }

     if (acker != null)
     {
         switch (role)
         {
             case 3:
                 {
                     Acaunt1 windowAkaunt = new Acaunt1();
                     windowAkaunt.Show();
                     Hide();
                     MessageBox.Show("ВЫ вошли в акаунт Админ");
                 }
                 break;

             case 2:
                 {
                     Acaunt2 windowAkaunt2 = new Acaunt2();
                     windowAkaunt2.Show();
                     Hide();
                     MessageBox.Show("ВЫ вошли в акаунт Менеджера");
                 }
                 break;

             case 1:
                 {
                     Acaunt3 windowAkaunt2 = new Acaunt3();
                     windowAkaunt2.Show();
                     Hide();
                     MessageBox.Show("ВЫ вошли в акаунт Клиент");
                 }
                 break;
         }

     }
     else
         MessageBox.Show("Вы ввели что-то не так!");
 }



public partial class Acaunt2 : Form
 {
     private string connection;
     private Model1 model;
     private Tovar tovar;
     public Acaunt2()
     {
         InitializeComponent();
         model = new Model1();
         model.Tovar.Load();
         tovarDataGrid(View).DataSource или DataContext = model.Tovar.Local.ToBindingList();
     }




private void button1_Click(object sender, EventArgs e)
{
    try
    {
        Tovar tovar = new Tovar()
        {
            ID_Tovar = int.Parse(IDTovar.Text),
            Name = Name1.Text,
            Cast = int.Parse(Cast1.Text),
     Data_Time = DateTime.Parse(DataTime.Text),

        };
        model.Tovar.Add(tovar);
        model.SaveChanges();
        model.Tovar.Load();
        tovarDataGridView.DataSource = model.Tovar.Local.ToBindingList();

    }
    catch (Exception p) 
    {
        MessageBox.Show("ФАТАЛИТИ: " + p.Message);
    }
}

