# SISTEMAS_DISTRIBUIDOS1
\\\ VEICULO
class Veiculo {

    int getAno() {
        throw new UnsupportedOperationException("Not supported yet."); // Generated from nbfs://nbhost/SystemFileSystem/Templates/Classes/Code/GeneratedMethodBody
    }
    
}


\\\ vEICULO Interface
import java.rmi.Remote;
import java.rmi.RemoteException;
import java.util.List;

/**
 *
 * @author SÁVIO FRANÇA
 */
public interface VeiculoInterface extends Remote {
    
    public List<Veiculo> search2Ano(int anoVeiculo) throws RemoteException;
    public void add(Veiculo v) throws RemoteException;
    
}




\\\Veiculo Server
import java.rmi.Naming;
import java.rmi.registry.LocateRegistry;

public class VeiculoServer {
    public static void main(String[] args) throws Exception {
        LocateRegistry.createRegistry(1099);
        
        VeiculoServerImpl veiculoServer = new VeiculoServerImpl();
        Naming.rebind("//Localhost/VeiculoServer", veiculoServer);
        
        System.out.println("Servidor de Veículo iniciado");
    }
    
}



\\\Veiculo Server IMPL
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;
import java.util.ArrayList;
import java.util.List;

/**
 *
 * @author SÁVIO FRANÇA
 */
public class VeiculoServerImpl extends UnicastRemoteObject implements VeiculoInterface {
    
    private List<Veiculo> veiculos;
    
    protected VeiculoServerImpl() throws RemoteException {
        super();
        this.veiculos = new ArrayList<>();
    }
    
    public List<Veiculo> search2Ano(int anoVeiculo) throws RemoteException {
        List<Veiculo> veiculosAno = new ArrayList<>();
        for (Veiculo v : veiculos) {
            if (v.getAno() == anoVeiculo) {
                veiculosAno.add(v);
            }
        }
        
        return veiculosAno;
    }

    public void add(Veiculo v) throws RemoteException {
        this.veiculos.add(v);
    }
    
}
