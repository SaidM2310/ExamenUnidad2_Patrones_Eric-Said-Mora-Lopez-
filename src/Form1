using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace examen
{
    public partial class Form1 : Form
    {
        private PoolJugadores pool;
        private Random rnd = new Random();
        
        public Form1()
        {
            InitializeComponent();

            // Permite detectar teclas desde el formulario
            this.KeyPreview = true;

            // Asignamos los eventos manualmente
            this.Load += Form1_Load;
            this.KeyDown += Form1_KeyDown;

            pool = new PoolJugadores();
        }

        private void Form1_Load(object sender, EventArgs e) //lobby
        {
            this.Text = "Lobby de jugadores";
            this.BackColor = System.Drawing.Color.WhiteSmoke;

            
            //creacion de botones
            Button btnAgregar = new Button();
            btnAgregar.Text = "conectar jugador";
            btnAgregar.Location = new System.Drawing.Point(350, 400);
            btnAgregar.Click += BtnAgregar_Click;
            this.Controls.Add(btnAgregar);

           
            Button btnDesconectar = new Button();
            btnDesconectar.Text = "Desconectar jugador";
            btnDesconectar.Location = new System.Drawing.Point(350, 20);
            btnDesconectar.Anchor = AnchorStyles.Top;
            btnDesconectar.Click += BtnDesconectar_Click;
            this.Controls.Add(btnDesconectar);
            CrearSalas();

        }
        private void CrearSalas()//salas
        {
          
            System.Drawing.Color colorSala = System.Drawing.Color.LightBlue;
            System.Drawing.Size tamañoSala = new System.Drawing.Size(150, 100);

            
            System.Drawing.Point[] posiciones = new System.Drawing.Point[]
            {
               new System.Drawing.Point(0, 0),//arriba izquierda
               new System.Drawing.Point(650, 0), //arriba derecha
               new System.Drawing.Point(0, 175), //medio izquierda
               new System.Drawing.Point(650, 175), //medio derecha
               new System.Drawing.Point(0, 350), //abajo izquierda
               new System.Drawing.Point(650, 350) //abajo derecha
            };

            for (int i = 0; i < posiciones.Length; i++)
            {
                Panel sala = new Panel();
                sala.Size = tamañoSala;
                sala.Location = posiciones[i];
                sala.BackColor = colorSala;
                sala.BorderStyle = BorderStyle.FixedSingle;

                Label label = new Label();
                label.Text = "Sala de juego";
                label.ForeColor = System.Drawing.Color.Black;
                label.Dock = DockStyle.Fill;
                label.TextAlign = System.Drawing.ContentAlignment.MiddleCenter;

                sala.Controls.Add(label);
                this.Controls.Add(sala);
                sala.BringToFront();
            }
        }


        private void BtnAgregar_Click(object sender, EventArgs e)//boton agregar jugador
        {
            Jugador j = pool.ObtenerJugador();
            if (j == null) return;

            j.Cuerpo.Location = new System.Drawing.Point(
                rnd.Next(180, 500),
                rnd.Next(0, 400)
            );
            this.Controls.Add(j.Cuerpo);
            j.Cuerpo.BringToFront();
        }
        private void BtnDesconectar_Click(object sender, EventArgs e)//boton desconectar jugador
        {
           
            var jugadoresActivos = pool.GetJugadoresEnUso();
            if (jugadoresActivos.Count == 0)
            {
                MessageBox.Show("No hay jugadores conectados.");
                return;
            }

            
            Jugador jugador = jugadoresActivos[jugadoresActivos.Count - 1];
            this.Controls.Remove(jugador.Cuerpo);
            pool.LiberarJugador(jugador);

        }

        private void Form1_KeyDown(object sender, KeyEventArgs e) //movimiento jugador
        {
            foreach (var jugador in pool.GetJugadoresEnUso())
            {
                jugador.Mover(e.KeyCode);
                DetectarEntradaASala(jugador);
            }
        }
        private void DetectarEntradaASala(Jugador jugador) //detectar cuando el jugador esta dentro de una sala
        {
            foreach (Control ctrl in this.Controls)
            {
                if (ctrl is Panel && ctrl.BackColor == System.Drawing.Color.LightBlue)
                {
                    if (jugador.Cuerpo.Bounds.IntersectsWith(ctrl.Bounds))
                    {
                        var servidor = ServidorPartida.Instancia;
                        Formsala sala = servidor.CrearSala(jugador);
                        sala.Show();
                        return;
                    }
                }
            }
        }

    }
}
